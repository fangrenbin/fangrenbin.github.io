---
author: fangrenbin
comments: true
date: 2014-07-05 13:03:51+00:00
layout: post
slug: spring-data-jpa-%e6%95%99%e7%a8%8b-%e7%ac%ac%e4%b8%80%e7%ab%a0%ef%bc%9a%e8%ae%be%e7%bd%ae
title: Spring Data JPA 教程 第一章：配置
wordpress_id: 628
categories:
- spring-data-jpa
---

本文属于翻译文章：
来源：
http://www.petrikainulainen.net/programming/spring-framework/spring-data-jpa-tutorial-part-one-configuration/

Spring Data JPA是一个简化创建JPA和减少与数据库交互代码的一个项目。我已经使用了一段时间，用在工作中和我自己的小项目中，它确实让事情变的更简单代码变的更干净。现在我要分享一下我的知识了。

这是第一部分的Spring Data JPA Tutorial，它将会告诉你如何设置Spring Data JPA，当你使用Hibernate作为JPA的提供者。在开始之前，我想说明一件事，本教程不是介绍如何使用Hibernate, JPA或者Spring。如果你想了解本教程的一些概念，你需要对这些内容有些了解。

下面是本教程需要的maven依赖：



	
  1. BoneCP 0.7.1.RELEASE（你也可以使用其它数据源实现）

	
  2. Hibernate 4.0.1.Final

	
  3. Spring Framework 3.1.0.RELEASE

	
  4. Spring Data JPA 1.0.2

	
  5. Servlet API 3.0



同时，我使用的是maven作为构建工具，如果你想运行这我的这个例子，你需要在你的电脑上面安装maven。



### 开始


下面是设置Spring Data JPA的步骤：
找到项目必要maven依赖
配置spring上下文，这些需要设置的bean为：数据源（datasource）,事务管理（transaction manager）和实体管理类（entity manager factory）。
下面是这几步的详细步骤：



### 获取项目依赖


首先，你需要获取到这些依赖。然后在你的pom.xml文件中加入它们，下面是我的例子中的pom.xml文件。


    
    
    <project xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://maven.apache.org/POM/4.0.0" xsi:schemalocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
        <modelversion>4.0.0</modelversion>
        <groupid>net.petrikainulainen.spring</groupid>
        <artifactid>data-jpa-tutorial-part-one</artifactid>
        <packaging>war</packaging>
        <version>0.1</version>
        <name>Spring Data JPA Tutorial Part One</name>
        <description>Spring Data JPA Tutorial Part One</description>
        <licenses>
            <license>
                <name>Apache License 2.0</name>
                <url>http://www.apache.org/licenses/LICENSE-2.0</url>
            </license>
        </licenses>
        <url>http://www.petrikainulainen.net</url>
        <repositories>
            <repository>
                <id>repository.jboss.org-public</id>
                <name>JBoss repository</name>
                <url>https://repository.jboss.org/nexus/content/groups/public</url>
            </repository>
        </repositories>
        <properties>
            <hibernate.version>4.0.1.Final</hibernate.version>
            <mysql.connector.version>5.1.18</mysql.connector.version>
            <slf4j.version>1.6.1</slf4j.version>
            <spring.version>3.1.0.RELEASE</spring.version>
            <project.build.sourceencoding>UTF-8</project.build.sourceencoding>
        </properties>
        <dependencies>
            
            <dependency>
                <groupid>org.springframework</groupid>
                <artifactid>spring-beans</artifactid>
                <version>${spring.version}</version>
            </dependency>
            <dependency>
                <groupid>org.springframework</groupid>
                <artifactid>spring-core</artifactid>
                <version>${spring.version}</version>
            </dependency>
            <dependency>
                <groupid>org.springframework</groupid>
                <artifactid>spring-context-support</artifactid>
                <version>${spring.version}</version>
            </dependency>
            <dependency>
                <groupid>org.springframework</groupid>
                <artifactid>spring-context</artifactid>
                <version>${spring.version}</version>
            </dependency>
            <dependency>
                <groupid>org.springframework</groupid>
                <artifactid>spring-jdbc</artifactid>
                <version>${spring.version}</version>
            </dependency>
            <dependency>
                <groupid>org.springframework</groupid>
                <artifactid>spring-orm</artifactid>
                <version>${spring.version}</version>
            </dependency>
            <dependency>
                <groupid>org.springframework</groupid>
                <artifactid>spring-tx</artifactid>
                <version>${spring.version}</version>
            </dependency>
            
            <dependency>
                <groupid>org.springframework</groupid>
                <artifactid>spring-web</artifactid>
                <version>${spring.version}</version>
            </dependency>
            <dependency>
                <groupid>org.springframework</groupid>
                <artifactid>spring-webmvc</artifactid>
                <version>${spring.version}</version>
            </dependency>
            <dependency>
                <groupid>cglib</groupid>
                <artifactid>cglib</artifactid>
                <version>2.2.2</version>
            </dependency>
            
            <dependency>
                <groupid>org.springframework.data</groupid>
                <artifactid>spring-data-jpa</artifactid>
                <version>1.0.2.RELEASE</version>
            </dependency>
            
            <dependency>
                <groupid>org.hibernate</groupid>
                <artifactid>hibernate-core</artifactid>
                <version>${hibernate.version}</version>
            </dependency>
            <dependency>
                <groupid>org.hibernate</groupid>
                <artifactid>hibernate-entitymanager</artifactid>
                <version>${hibernate.version}</version>
            </dependency>
            
            <dependency>
                <groupid>com.h2database</groupid>
                <artifactid>h2</artifactid>
                <version>1.3.160</version>
            </dependency>
            
            
            
            
            
            
            
            <dependency>
                <groupid>com.jolbox</groupid>
                <artifactid>bonecp</artifactid>
                <version>0.7.1.RELEASE</version>
            </dependency>
            
            <dependency>
                <groupid>javax.servlet</groupid>
                <artifactid>javax.servlet-api</artifactid>
                <version>3.0.1</version>
                <scope>provided</scope>
            </dependency>
            <dependency>
                <groupid>javax.servlet</groupid>
                <artifactid>jstl</artifactid>
                <version>1.2</version>
            </dependency>
            
            <dependency>
                <groupid>org.slf4j</groupid>
                <artifactid>slf4j-api</artifactid>
                <version>${slf4j.version}</version>
            </dependency>
            <dependency>
                <groupid>org.slf4j</groupid>
                <artifactid>slf4j-log4j12</artifactid>
                <version>${slf4j.version}</version>
            </dependency>
            <dependency>
                <groupid>log4j</groupid>
                <artifactid>log4j</artifactid>
                <version>1.2.16</version>
            </dependency>
            
            <dependency>
                <groupid>junit</groupid>
                <artifactid>junit</artifactid>
                <version>4.9</version>
                <scope>test</scope>
            </dependency>
        </dependencies>
        <build>
            <finalname>data-jpa-tutorial-part-one</finalname>
            <plugins>
                <plugin>
                    <groupid>org.apache.maven.plugins</groupid>
                    <artifactid>maven-compiler-plugin</artifactid>
                    <version>2.3.2</version>
                    <configuration>
                        <source>1.6</source>
                        <target>1.6</target>
                    </configuration>
                </plugin>
                <plugin>
                    <groupid>org.apache.maven.plugins</groupid>
                    <artifactid>maven-war-plugin</artifactid>
                    <version>2.1.1</version>
                    <configuration>
                        <failonmissingwebxml>false</failonmissingwebxml>
                    </configuration>
                </plugin>
                <plugin>
                    <groupid>org.mortbay.jetty</groupid>
                    <artifactid>jetty-maven-plugin</artifactid>
                    <version>8.1.0.RC2</version>
                    <configuration>
                        <scanintervalseconds>0</scanintervalseconds>
                        <webappconfig>
                            <defaultsdescriptor>src/main/resources/webdefault.xml</defaultsdescriptor>
                        </webappconfig>
                    </configuration>
                </plugin>
                <plugin>
                    <groupid>org.apache.maven.plugins</groupid>
                    <artifactid>maven-site-plugin</artifactid>
                    <version>3.0</version>
                    <configuration>
                        <reportplugins>
                            
                            <plugin>
                                <groupid>org.codehaus.mojo</groupid>
                                <artifactid>cobertura-maven-plugin</artifactid>
                                <version>2.5.1</version>
                            </plugin>
                        </reportplugins>
                    </configuration>
                </plugin>
            </plugins>
        </build>
    </project>
    





### 配置Spring应用的上下文


第二，你需要配置Spring应用的上下文。可能你可记得，你需要配置数据源（datasource），事务管理（transaction manager），实体类管理（entity manager）的bean。如果你使用的是Spring 3.1和Servlet 3.0，你可以使用Java类来实现然后在web应用初始化的时候载入这些配置信息。我的这边配置类如下：

    
    
    import com.jolbox.bonecp.BoneCPDataSource;
    import org.hibernate.ejb.HibernatePersistence;
    import org.springframework.context.MessageSource;
    import org.springframework.context.annotation.*;
    import org.springframework.context.support.ResourceBundleMessageSource;
    import org.springframework.core.env.Environment;
    import org.springframework.orm.jpa.JpaTransactionManager;
    import org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean;
    import org.springframework.web.servlet.ViewResolver;
    import org.springframework.web.servlet.config.annotation.EnableWebMvc;
    import org.springframework.web.servlet.view.InternalResourceViewResolver;
    import org.springframework.web.servlet.view.JstlView;
     
    import javax.annotation.Resource;
    import javax.sql.DataSource;
     
    /**
     * An application context Java configuration class. The usage of Java configuration
     * requires Spring Framework 3.0 or higher with following exceptions:
     * <ul>
     *     <li>@EnableWebMvc annotation requires Spring Framework 3.1</li>
     * </ul>
     * @author Petri Kainulainen
     */
    @Configuration
    @ComponentScan(basePackages = {"net.petrikainulainen.spring.datajpa.controller"})
    @EnableWebMvc
    @ImportResource("classpath:applicationContext.xml")
    @PropertySource("classpath:application.properties")
    public class ApplicationContext {
         
        private static final String VIEW_RESOLVER_PREFIX = "/WEB-INF/jsp/";
        private static final String VIEW_RESOLVER_SUFFIX = ".jsp";
     
        private static final String PROPERTY_NAME_DATABASE_DRIVER = "db.driver";
        private static final String PROPERTY_NAME_DATABASE_PASSWORD = "db.password";
        private static final String PROPERTY_NAME_DATABASE_URL = "db.url";
        private static final String PROPERTY_NAME_DATABASE_USERNAME = "db.username";
     
        private static final String PROPERTY_NAME_HIBERNATE_DIALECT = "hibernate.dialect";
        private static final String PROPERTY_NAME_HIBERNATE_FORMAT_SQL = "hibernate.format_sql";
        private static final String PROPERTY_NAME_HIBERNATE_NAMING_STRATEGY = "hibernate.ejb.naming_strategy";
        private static final String PROPERTY_NAME_HIBERNATE_SHOW_SQL = "hibernate.show_sql";
        private static final String PROPERTY_NAME_ENTITYMANAGER_PACKAGES_TO_SCAN = "entitymanager.packages.to.scan";
     
        private static final String PROPERTY_NAME_MESSAGESOURCE_BASENAME = "message.source.basename";
        private static final String PROPERTY_NAME_MESSAGESOURCE_USE_CODE_AS_DEFAULT_MESSAGE = "message.source.use.code.as.default.message";
     
        @Resource
        private Environment environment;
     
        @Bean
        public DataSource dataSource() {
            BoneCPDataSource dataSource = new BoneCPDataSource();
     
            dataSource.setDriverClass(environment.getRequiredProperty(PROPERTY_NAME_DATABASE_DRIVER));
            dataSource.setJdbcUrl(environment.getRequiredProperty(PROPERTY_NAME_DATABASE_URL));
            dataSource.setUsername(environment.getRequiredProperty(PROPERTY_NAME_DATABASE_USERNAME));
            dataSource.setPassword(environment.getRequiredProperty(PROPERTY_NAME_DATABASE_PASSWORD));
     
            return dataSource;
        }
     
        @Bean
        public JpaTransactionManager transactionManager() throws ClassNotFoundException {
            JpaTransactionManager transactionManager = new JpaTransactionManager();
     
            transactionManager.setEntityManagerFactory(entityManagerFactoryBean().getObject());
     
            return transactionManager;
        }
     
        @Bean
        public LocalContainerEntityManagerFactoryBean entityManagerFactoryBean() throws ClassNotFoundException {
            LocalContainerEntityManagerFactoryBean entityManagerFactoryBean = new LocalContainerEntityManagerFactoryBean();
     
            entityManagerFactoryBean.setDataSource(dataSource());
            entityManagerFactoryBean.setPackagesToScan(environment.getRequiredProperty(PROPERTY_NAME_ENTITYMANAGER_PACKAGES_TO_SCAN));
            entityManagerFactoryBean.setPersistenceProviderClass(HibernatePersistence.class);
     
            Properties jpaProterties = new Properties();
            jpaProterties.put(PROPERTY_NAME_HIBERNATE_DIALECT, environment.getRequiredProperty(PROPERTY_NAME_HIBERNATE_DIALECT));
            jpaProterties.put(PROPERTY_NAME_HIBERNATE_FORMAT_SQL, environment.getRequiredProperty(PROPERTY_NAME_HIBERNATE_FORMAT_SQL));
            jpaProterties.put(PROPERTY_NAME_HIBERNATE_NAMING_STRATEGY, environment.getRequiredProperty(PROPERTY_NAME_HIBERNATE_NAMING_STRATEGY));
            jpaProterties.put(PROPERTY_NAME_HIBERNATE_SHOW_SQL, environment.getRequiredProperty(PROPERTY_NAME_HIBERNATE_SHOW_SQL));
     
            entityManagerFactoryBean.setJpaProperties(jpaProterties);
     
            return entityManagerFactoryBean;
        }
     
        @Bean
        public MessageSource messageSource() {
            ResourceBundleMessageSource messageSource = new ResourceBundleMessageSource();
     
            messageSource.setBasename(environment.getRequiredProperty(PROPERTY_NAME_MESSAGESOURCE_BASENAME));
            messageSource.setUseCodeAsDefaultMessage(Boolean.parseBoolean(environment.getRequiredProperty(PROPERTY_NAME_MESSAGESOURCE_USE_CODE_AS_DEFAULT_MESSAGE)));
     
            return messageSource;
        }
     
        @Bean
        public ViewResolver viewResolver() {
            InternalResourceViewResolver viewResolver = new InternalResourceViewResolver();
     
            viewResolver.setViewClass(JstlView.class);
            viewResolver.setPrefix(VIEW_RESOLVER_PREFIX);
            viewResolver.setSuffix(VIEW_RESOLVER_SUFFIX);
     
            return viewResolver;
        }
    }
    


我的web应用初始化工具如下：

    
    
    import org.springframework.web.WebApplicationInitializer;
    import org.springframework.web.context.ContextLoaderListener;
    import org.springframework.web.context.support.AnnotationConfigWebApplicationContext;
    import org.springframework.web.servlet.DispatcherServlet;
     
    import javax.servlet.*;
     
    /**
     * Web application Java configuration class. The usage of web application
     * initializer requires Spring Framework 3.1 and Servlet 3.0.
     * @author Petri Kainulainen
     */
    public class DataJPAExampleInitializer implements WebApplicationInitializer {
         
        private static final String DISPATCHER_SERVLET_NAME = "dispatcher";
        private static final String DISPATCHER_SERVLET_MAPPING = "/";
         
        @Override
        public void onStartup(ServletContext servletContext) throws ServletException {
            AnnotationConfigWebApplicationContext rootContext = new AnnotationConfigWebApplicationContext();
            rootContext.register(ApplicationContext.class);
     
            ServletRegistration.Dynamic dispatcher = servletContext.addServlet(DISPATCHER_SERVLET_NAME, new DispatcherServlet(rootContext));
            dispatcher.setLoadOnStartup(1);
            dispatcher.addMapping(DISPATCHER_SERVLET_MAPPING);
     
            servletContext.addListener(new ContextLoaderListener(rootContext));
        }
    }
    


你也许注意到我使用@PropertySource注解来指定配置中需要的值的文件。下面是application.properties文件的内容：

    
    
    # The default database is H2 memory database but I have also
    # added configuration needed to use either MySQL and PostgreSQL.
     
    #Database Configuration
    db.driver=org.h2.Driver
    #db.driver=com.mysql.jdbc.Driver
    #db.driver=org.postgresql.Driver
    db.url=jdbc:h2:mem:datajpa
    #db.url=jdbc:mysql://localhost:3306/datajpa
    #db.url=jdbc:postgresql://localhost/datajpa
    db.username=sa
    db.password=
     
    #Hibernate Configuration
    hibernate.dialect=org.hibernate.dialect.H2Dialect
    #hibernate.dialect=org.hibernate.dialect.MySQL5InnoDBDialect
    #hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
    hibernate.format_sql=true
    hibernate.ejb.naming_strategy=org.hibernate.cfg.ImprovedNamingStrategy
    hibernate.show_sql=true
     
    #MessageSource
    message.source.basename=i18n/messages
    message.source.use.code.as.default.message=true
     
    #EntityManager
    #Declares the base package of the entity classes
    entitymanager.packages.to.scan=net.petrikainulainen.spring.datajpa.model
    





### 配置Spring Data JPA


第三步，你需设置Spring Data JPA。如果你刚才比较细心，应该注意到我在应用配置类中使用 @ImportResource注解来导入XML配置文件。当前，Spring Data JPA不支持使用Java类来配置。因此，只有一种方法，就是使用XML配置文件。我的applicationContext.xml如下：

    
    
    
    <beans xmlns:mvc="http://www.springframework.org/schema/mvc" xmlns:jpa="http://www.springframework.org/schema/data/jpa" xmlns="http://www.springframework.org/schema/beans" xsi:schemalocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.1.xsd
            http://www.springframework.org/schema/data/jpa http://www.springframework.org/schema/data/jpa/spring-jpa-1.0.xsd
            http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-3.1.xsd" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        
        <mvc:resources mapping="/static/**" location="/static/"></mvc:resources>
     
        
        <mvc:default-servlet-handler></mvc:default-servlet-handler>
     
        
        <jpa:repositories base-package="net.petrikainulainen.spring.datajpa.repository"></jpa:repositories>
    </beans>
    




### 完成


就这样，我已经给你做了一个示范，告诉你如何来配置Spring Data JPA。同时，我也创建了一个示例程序来证明这个配置程序是能够运行的。你从我的[Githu](https://github.com/pkainulainen/spring-data-jpa-examples/tree/master/tutorial-part-one)上面把代码拿下来，然后自己测试一下，用Mavne Jetty插件来运行一下这个web应用。（提示：记得先创建model和repository包）。













