---
layout: post
title: Spring MVC 구조
subtitle: BackEnd study
categories: BackEnd
tags: [backend, mvc, spring]
---

### Spring MVC (Model View Controller)
Spring MVC는 mvc 패턴기반의 웹 프레임워크다.


## Model
어플리케이션 정보, 데이터 처리관리. Dao, Dto, Service로 나눌수 있다
* 사용자가 사용하는 모든 데이터 정보를 가지고있는 컴포넌트이며, View나 Controller의 어떤 정보도 알수없어야한다.
* DB 와 연동하여 사용자가 입력한 데이터나 출력할 데이터를 다룬다
* 변경이 일어나면 처리방법을 구현해야한다

{: .box-Dao}
### Dao (Data Access Object)
DB를 사용해 데이터를 조회하거나 조작하는 기능을 담당하는 것들을 DAO라고 부른다. domain logic(DB와 관련없는 코드들)을 persistence mechanism과 분리하기 위해 사용한다. 

UserDao.java
---java

public interface UserDao {
    /**
     * user 테이블에서 모든 유저의 정보를 가져온다.
     * 
     * @return 모든 유저의 정보
     */
    public List<User> getUsers();
}
---

UserDaoImpl.java
---java
@Repository("userDao")
public class UserDaoImpl implements UserDao {
    @Override
    public List<User> getUsers()
    {
        // 리스트 생성
        List<User> result = new ArrayList<User>();

        // 데이터베이스에서 유저 목록을 가져온다.
        result.add(...);
        ...

        return result;
    }
}
---

{: .box-Dto}
### Dto (Data Transfer Object)
VO(Value Object)라고도 표현함, 계층간 데이터 교환을 위한 Java Beans. 보통 로직을 가지고 있지 않고 data와 그 data에 접근을 위한 getter, setter만 가지고 있다.
Database에서 Data를 얻어 Service나 Controller 등으로 보낼 때 사용하는 객체를 말한다. 
---java
public class User {
    private String name;
    private int age;

    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void getAge() {
        return this.age;
    }

    public void setAge(int age)
    {
        this.age = age;
    }

    @Override
    public String toString() {
        return "name='" + name + "', age=" + age;
    }
}
---


{: .box-Service}
### Service
Service는 비지니스 로직이 들어가는 부분이다. Controller가 Request를 받으면 적절한 Service에 전달하고, 전달 받은 Service는 비즈니스 로직을 처리한다. DAO로 데이터베이스를 접근하고, DTO로 데이터를 전달받은 다음, 적절한 처리를 해 반환한다.
---java
public interface UserService {
    /**
     * 유저 정보를 텍스트 파일로 저장한다.
     * 
     * @param path 저장할 파일의 경로
     * @return 저장한 유저의 개수
     */
    public int saveUsersAsTextFile(String path);
}
---

---java
@Service("userService")
public class UserServiceImpl implements UserService {
    private static final Logger LOGGER = Logger.getLogger("UserServiceImpl");

    @Autowired
    private UserDao userDao;

    @Override
    public int saveUsersAsTextFile(String path) {
        List<User> users = userDao.getUsers();

        // 비즈니스 로직
        try (FileOutputStream fileOutputStream = new FileOutputStream(path)) {
            StringBuilder result = new StringBuilder();
            for(User user : users) {
                result.append(user);
                result.append('\n');
            }

            fileOutputStream.write(result.toString().getBytes());
        } catch (IOException exception) {
            LOGGER.log(Level.SEVERE, "파일을 쓸 수 없습니다.");
            throw new IllegalStateException(String.format("Can't write a file. path: %s", path));
        }

        return users.size();
    }
}
---
위 코드는 DAO로부터 DTO 리스트를 받고, DTO의 리스트를 파일로 저장하는 코드이다. @Autowired annotation으로 userDao bean을 찾아서 연결한 것을 볼 수 있다. (Spring에서는 DI(Dependency Injection, 의존성 주입)이라고 한다.)

Controller에서 서비스 호출은 아래 코드처럼 쓰일 수 있다.
---java
@Controller
public class MainController {
    @Autowired
    private UserService userService;

    @RequestMapping(value = "/save/users", method = RequestMethod.GET)
    public ModelAndView saveUsers(ModelAndView mv) {
        // 유저를 얻어와서 텍스트 파일로 저장한다.
        int saveCount = userService.saveUsersAsTextFile("users.txt");

        // 뷰에서 결과를 보여주기 위해 저장한 개수를 뷰에 넘긴다.
        mv.addObject("saveCount", saveCount);
        mv.setViewName("saveUsersResultView");

        return mv;
    }
}
---

코드 출처 https://lazymankook.tistory.com/30





## View
사용자 인터페이스, 사용자에게 보여짐
* Model이 가지고있는 데이터를 저장하면 안된다
* Model이나 Controller의 정보를 알면 안되며 단순히 표시해주는 역할을 가지고있다
* 변경이 일어나면 처리방법을 구현해야한다

## Controller
Model과 View간의 상호동작 조정과 연결
*Model 또는 View에 대한 정보를 알아야한다
*model 또는 View의 변경을 인지하여 대처를 해야한다


### Component 정리
| ----- | ----- |
| DispatcherServlet | 모든 요청을 최초로 받아들이는 역할 |
| Controller | 요청을 실제로 처리하는 역할 |
| HandlerMapping | 클라이언트 요청을 처리할 Controller를 찾는 작업처리 |
| View | 응답하는 로직을 처리 |
| ViewPeslover | 응답할 View를 찾는 작업을 처리 |
| ModelAndView | 컨트롤러의 처리결과로써 응답에 사용할 데이터와 뷰에대한 정보 집합 |



