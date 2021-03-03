spring 2일차

* 화면에 DataBase의 시간을 표출해 본다 
1. 순수 JDBC 연결 확인

	
//		JDBC 드라이버 확인

		Class.forName("com.mysql.cj.jdbc.Driver");
		
		log.info("1------------------------");
		
		String url = "jdbc:mysql://localhost:3306/dclass?serverTimezone=UTC";
		String username = "springuser";
		String password = "springuser";
		
//		커넥션 확인

		Connection con = DriverManager.getConnection(url, username, password);
		
		log.info(con);
		
		con.close();
2. HikariCP 세팅 - root-context.xml 혹은 Java설정<br>

<!-- Root Context: defines shared resources visible to all other web components -->
	<bean id="hikariConfig" class="com.zaxxer.hikari.HikariConfig">
		<property name="driverClassName" value="com.mysql.cj.jdbc.Drive"></property>
		<property name="jdbcUrl" value="jdbc:mysql://localhost:3306/dclass?serverTimezone=UTC"></property>
		<property name="username" value="springuser"></property>
		<property name="password" value="springuser"></property>
	</bean>

	<!-- HikariCP configuration -->
	<bean id="dataSource" class="com.zaxxer.hikari.HikariDataSource"
		destroy-method="close">
		<constructor-arg ref="hikariConfig" />  
	</bean>	
HikariCP git 주소: https://github.com/brettwooldridge/HikariCP

3. Spring 이용해서 확인

4. DAO제작
-테스트(Junit)


5. HomeController에 주입 / 확인


Mybatis(미니멈) 셋팅

1. maven 추가<br>
	(1) https://mvnrepository.com/artifact/org.mybatis/mybatis <br>
	(2) https://mvnrepository.com/artifact/org.mybatis/mybatis-spring<br>
2. root-context.xml 라이브러리 추가
	<bean id="sqlSessionFactory"
		class="org.mybatis.spring.SqlSessionFactoryBean">
		<property name="dataSource" ref="dataSource"></property>
	</bean>
3. 
