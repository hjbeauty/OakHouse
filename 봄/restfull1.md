---
description: Spring Restfull
---

# Rest API

## Hello Restfull 출력하기   .

RestController를 작성한    .

```java
package com.bit.oakhouse.controller;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/hello")
public class SpringRestController {
	@RequestMapping(value = "/{name}", method = RequestMethod.GET)
	public String hello(@PathVariable String name) {
		String result="Hello "+name; 
		return result;
	}
}
```

@PathVariable : URL에서 메소드 매개변수로 값을 삽입하는데 사용된다. {name} ==&gt; String name에 대입  .

@ResponseBody : Spring3에서는 return자리에 사용했지만, Spring 4이상에서는 @RestController 만 적어주면 된다  .

```java
@RestController = @Controller + @ResponseBody
```

JSP파일없이 브라우저에서 확인할 수있다  .

