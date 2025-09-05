SpringBoot
1.打包后引入依赖
```
        <dependency>
            <groupId>org.xhy</groupId>
            <artifactId>xhy-web-starter</artifactId>
            <version>1.0.0</version>
        </dependency>
```
2.启动

拓展点 1.WebMvcConfigurer 用于配置拦截器，全局转换器
```
@EnableWebMvc
@Component
public class WebMvc implements WebMvcConfigurer {

    @Override
    public void addInterceptor(InterceptorRegistry registry) {
        registry.addInterceptor(new DemoInterceptor()).addIncludePatterns("/order/**");
    }
}
```
2.全局异常/类型转换 类上标注``@ControllerAdvice/@RestControllerAdvice``
```
@RestControllerAdvice
public class DemoControllerAdvice {
	// 注解中写捕获的异常	
    @ExceptionHandler(Exception.class)
    public String ex(Exception e){
        return e.getMessage();
    }
	// 注解中需要转换的类,方法参数必须写Object
    @ConvertType(Byte.class)
    public String byteConvert(Object value){
        return value.toString();
    }
}
```
3.局部异常/类型转换 在Controller当中创建方法标注注解
```
@ExceptionHandler(Exception.class)
    public String ex(Exception e){
        return e.getMessage();
    }
    @ConvertType(Integer.class)
    public Object c(Object o){
        return o;
    }
```
