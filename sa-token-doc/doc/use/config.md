# 框架配置
- 你可以零配置启动框架
- 但同时你也可以通过配置，定制性使用框架，sa-token支持多种方式配置框架信息

--- 
### 所有可配置项
| 参数名称	| 类型		| 默认值		| 说明																				|
| :--------	| :--------	| :--------	| :--------																			|
| tokenName	| String	| satoken	| token名称（同时也是cookie名称）													|
| timeout	| long		| 2592000	| token有效期，单位s 默认30天，-1为永不过期											|
| isShare	| Boolean	| true		|  在多人登录同一账号时，是否共享会话（为true时共用一个，为false时新登录挤掉旧登录）	|
| isReadHead| Boolean	| true		| 是否在cookie读取不到token时，继续从请求header里继续尝试读取							|
| isReadBody| Boolean	| true		| 是否在header读取不到token时，继续从请求题参数里继续尝试读取						|
| isV		| Boolean	| true		| 是否在初始化配置时打印版本字符画													|





### 方式1、通过代码配置
``` java 
	/**
	 * sa-token代码方式进行配置
	 */
	@Configuration
	public class MySaTokenConfig {
	
		// 获取配置Bean 
		@Primary
		@Bean(name="MySaTokenConfig")
		public SaTokenConfig getSaTokenConfig() {
			SaTokenConfig config = new SaTokenConfig();
			config.setTokenName("satoken");		// token名称（同时也是cookie名称）
			config.setTimeout(30 * 24 * 60 * 60); 	// token有效期，单位s 默认30天，-1为永不过期   
			config.setIsShare(true);				// 在多人登录同一账号时，是否共享会话（为true时共用一个，为false时新登录挤掉旧登录）
			config.setIsReadHead(true);		// 是否在cookie读取不到token时，继续从请求header里继续尝试读取 
			config.setIsReadBody(true);		// 是否在cookie读取不到token时，继续从请求header里继续尝试读取 
			config.setIsV(true);					// 是否在初始化配置时打印版本字符画
			return config;
		}
		
	}
```

### 方式2、在`application.yml`配置

``` java
spring: 
    # sa-token配置
    sa-token: 
        # token名称（同时也是cookie名称）
        token-name: satoken
        # token有效期，单位s 默认30天，-1为永不过期   
        timeout: 2592000
        # 在多人登录同一账号时，是否共享会话（为true时共用一个，为false时新登录挤掉旧登录）
        is-share: true
        # 是否在cookie读取不到token时，继续从请求header里继续尝试读取 
        is-read-head: true
        #  是否在header读取不到token时，继续从请求题参数里继续尝试读取 
        is-read-body: true
        # 是否在初始化配置时打印版本字符画
        is-v: true
```

- 如果你习惯于 `application.properties` 类型的配置文件，那也很好办: 
- 百度： [springboot properties与yml 配置文件的区别](https://www.baidu.com/s?ie=UTF-8&wd=springboot%20properties%E4%B8%8Eyml%20%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E7%9A%84%E5%8C%BA%E5%88%AB)


