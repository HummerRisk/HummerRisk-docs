
### Spring Security

!!! info "项目地址"
    * Github 项目地址：https://github.com/spring-projects/spring-security
    * Spring Security 官方文档：https://spring.io/projects/spring-security

#### 一、Spring Security 是什么

!!! abstract "安全框架 Spring Security 是什么"
    1. Spring Security 是一套认证授权框架, 支持认证模式如 HTTP BASIC 认证头 (基于 IETF RFC-based 标准), HTTP Digest 认证头 ( IETF RFC-based 标准), Form-based authentication (用于简单的用户界面), OpenID 认证等, Spring Security使得当前系统可以快速集成这些验证机制亦或是实现自己的一套验证机制.
    1. Spring Security 是⼀个功能强大、可高度定制的身份验证和访问控制框架。它是保护基于 Spring 的应用程序的事实标准。
    2. Spring Security 是⼀个面向Java应用程序框架。与所有Spring项目⼀样，Spring Security 的真正威力在于它可以轻松地扩展以满足定制需求。

![Kube-Bench](../../img/related/spring-security/img.png){ width="95%" }


#### 二、权限管理

!!! abstract "认证和授权"
    在Spring Security中，权限管理主要包括两个方面：认证和授权。简单来说，认证就是用户的登录认证；授权就是登录成功之后，用户可以访问资源的多少。
    
!!! warning "什么是认证和授权"
    1. 什么是权限管理
        * 基本上涉及到用户参与的系统都要进行权限管理，权限管理属于系统安全的范畴，权限管理实现对用户访问系统的控制 ，按照安全规则 或者 安全策略控制用户 可以访问而且只能访问自己被授权的资源。权限管理包括用户身份认证和授权两部分，简称认证授权。对于需要访问控制的资源用户首先经过身份认证，认证通过后用户具有该资源的访问权限才可访问。
    2. 什么是认证
        * 认证 ，就是判断⼀个用户是否为合法用户的处理过程。最常用的简单身份认证方式是系统通过核对用户输入的用户名和口令（密码），看其是否与系统中存储的该用户的用户名和口令⼀致，来判断用户身份是否正确。这就好比我们登录QQ、微信、游戏账号等等需要的账号和密码~
    3. 什么是授权
        * 授权 ，即访问控制，控制谁能访问哪些资源。主体进行身份认证后需要分配权限才可访问系统的资源，对于某些资源没有权限是无法访问的。这就好比学校的网站，有学生可以访问的资源，然而老师的资源学生就无法访问~


    
