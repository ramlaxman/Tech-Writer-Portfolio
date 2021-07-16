Firstly,

Extract the tomcat directory on desired location.

Run The Command,

/home/mayur/apache-tomcat-7.0.19/bin/startup.sh

Now Tomcat starts.

Now,the real task starts. It is not like window that to put files in webapps and start working.

For JSP,

Choose the folder inside the webapps directory i.e.

 http://localhost:8080/examples/All/RAM.jsp

Now  its Nice!!

We have to go for Servlet,

In this we have to touch the main directory i.e.

http://localhost:8080/examples/servlets/servlet/hi

We have to make entry into main web.xml which is at the location

/webapps/examples/WEB-INF/

<servlet>
        <servlet-name>hi</servlet-name>
        <servlet-class>hi</servlet-class>
    </servlet>
<servlet-mapping>
        <servlet-name>hi</servlet-name>
        <url-pattern>/servlets/servlet/hi</url-pattern>
    </servlet-mapping>


And class files are present at the location

webapps/examples/WEB-INF/classes/*.class files.
