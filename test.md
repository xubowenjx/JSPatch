# 数据源检查

##  1.检查oracle-ds.xml
 >位置：dbsjkf10380/deploy
 
找到自己的数据源。没有加上。
 ```xml
 <local-tx-datasource>
    <jndi-name>/ls/uap/bpm</jndi-name>
    <use-java-context>false</use-java-context>
    <connection-url>jdbc:oracle:thin:@172.19.188.198:1521:memdev</connection-url>
    <driver-class>oracle.jdbc.driver.OracleDriver</driver-class>
    <user-name>lspf_bpm</user-name>
    <password>lspf_bpm</password>
    <exception-sorter-class-name>
      org.jboss.resource.adapter.jdbc.vendor.OracleExceptionSorter
    </exception-sorter-class-name>
    <metadata>
       <type-mapping>Oracle11g</type-mapping>
    </metadata>
  </local-tx-datasource>  
 ```
## 2.检查datasource.xml
 >位置：amber2_server.war/WEB-INF/configuration
 
 没有自己配上。
 
 ```xml
 
 <constructor-arg>
			<map>
				<entry key="default" value-ref="dataSource"/>
				<entry key="defaultbpm" value-ref="dataSourcebpm"/>
				<entry key="defaulti18n" value-ref="dataSourcei18n"/>
				<entry key="mdm_vee" value-ref="dataSourcemdmvee"/>
				<entry key="mdm_gom" value-ref="dataSourcemdmgom"/>
				<entry key="mdm" value-ref="dataSourcemdm"/>
				<entry key="cis_ca" value-ref="dataSourcecisca"/>
				<entry key="cis_am" value-ref="dataSourcecisam"/>
				<entry key="mdm_llm" value-ref="dataSourcemdmllm"/>
				<entry key="mdm_mrm" value-ref="dataSourcemdmmrm"/>
				<entry key="sp_ce" value-ref="dataSourcespce"/>
				<entry key="sp_cm" value-ref="dataSourceSpcm"/>


			    <!--   <entry key="mysql" value-ref="dataSourceMysql"/> -->
			</map>
		</constructor-arg>
        
 ```
 
##   3.检查自己包中引用的数据源是否正确
 
##   4.dataSource.xml添加数据源
 *  方式1
 引用oracle-ds.xml中的jndi-name
 ```xml
 
 <bean id="dataSourcebpm" class="com.ls.pf.base.common.persistence.manager.DataSourceConnection">
		<constructor-arg value="ls/uap/bpm">
	 	</constructor-arg>
	</bean>
    
 ```
 * 方式2
 直接在dataSource.xml中配置,`配置记得加到map中`
 ```
 <bean id="dataSourcespce" class="org.apache.commons.dbcp.BasicDataSource"
		destroy-method="close">
		<property name="driverClassName" value="oracle.jdbc.driver.OracleDriver"/>
		<property name="url" value="jdbc:oracle:thin:@172.19.188.198:1521:memdev"/>
		<property name="username" value="sp_ce"/>
		<property name="password" value="sp_ce"/>
		<property name="maxActive" value="100" />
		<property name="maxIdle" value="30" />
		<property name="maxWait" value="5000" />
		<property name="defaultAutoCommit" value="true" />
		<property name="removeAbandoned" value="true" />
		<property name="removeAbandonedTimeout" value="60" />
		<property name="logAbandoned" value="true" />
	</bean>	
    
 ```
 

 

