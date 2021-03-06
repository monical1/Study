## `@SessionAttributes`、`@SessionAttribute`、`@ModelAttribue`用法

* `@SessionAttributes` - 只能用于控制器类上，需配合`ModelAttribute`使用
* `@SessionAttribute` - 用于方法参数前
* `@ModelAttribute` - 既可以用于方法参数前，也可以用在方法上

### 保存`session`

```java
@RequestMapping("/")
public String index(HttpSession session) {
    User user = new User();
    user.setId(1L);
    user.setUsername("zhangsan");
    user.setPassword("123456");
    session.setAttribute("user", user);
    return "index";
}
```

### 获取`session`封装为`JavaBean`

> 方式一

```java
@RequestMapping("/session1")
@ResponseBody
public String t1(@SessionAttribute("user") User user) {
    return user.toString();
}
```

> 方式二（`@SessionAttributes`和`@ModelAttribute`同时使用才能获取到）

```java
@Controller
@SessionAttributes("user")
public class IndexController {

    // 这种方法必须是session中对象已经存在，否则会报错
    // 定义一个空值
    @ModelAttribute("user")
    public String populateForm() {
        return null; // populates form for the first time if its null
    }

    @RequestMapping("/session2")
    @ResponseBody
    public String t(@ModelAttribute("user") User user) {
        return user.toString();
    }
}
```
