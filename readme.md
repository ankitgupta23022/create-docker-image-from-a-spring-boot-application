In dockerfile

FROM openjdk:11
ARG JAR_FILE=target/*.jar
COPY ${JAR_FILE} user-service.jar
ENTRYPOINT ["java","-jar","/user-service.jar"]

In the same path:-

docker build -t user-service.jar .

To check the images:-

docker images

To run the image:-

docker run -p 8081:8081 user-service.jar

To push the image to the Docker Hub:-

docker login
Give Username
Give Password

Before pushing tag the docker image:-

docker tag user-service.jar ankit23022/user-service.jar

Check whether it got tagged or not by running:-

Docker images

Now push the image to docker hub:-

docker push ankit23022/user-service.jar

Image is pushed to docker hub..


To pull the image we fromm docker hub we use:-

docker pull ankit23022/user-service.jar

To run the pulled image from dockerhub we use:-

docker run -p 8082:8081 ankit23022/user-service.jar



----------------------------------------------------------------------

Easy way:- 

Launch your docker terminal

Include docker dependency plugin in your pom.xml 

<plugin>
				<groupId>com.spotify</groupId>
				<artifactId>dockerfile-maven-plugin</artifactId>
				<version>1.4.13</version>
				<executions>
					<execution>
						<id>default</id>
						<goals>
							<goal>build</goal>
							<goal>push</goal>
						</goals>
					</execution>
				</executions>
				<configuration>
					<repository>ankit23022/${project.artifactId}</repository>
					<tag>${project.version}</tag>
					<buildArgs>
						<JAR_FILE>target/${project.build.finalName}.jar</JAR_FILE>
					</buildArgs>
				</configuration>
			</plugin>

and 

Do maven clean +

Do maven install, it'll build the image

You can look up this image with the command:- docker images from the terminal

And with the help of the image tag we can push our image to docker hub:-

docker push ankit23022/user-service:0.0.1-SNAPSHOT

To pull the image we can use:-

docker pull ankit23022/user-service:0.0.1-SNAPSHOT

To run the same image we can use:-

docker run -p 8082:8081 ankit23022/user-service:0.0.1-SNAPSHOT


-----------------------------------------------


Another way(Didnt work for me tho):-

Add Developer tool dependency

Go to the directory and run this command in the terminal

mvn spring-boot:build-image

This command will create an image of your application, you can now push this to DockerHUB


------------------------------------------------

Another way is using Google JIB (Doesn't require docker installed on your system)

<plugin>
  <groupId>com.google.cloud.tools</groupId>
  <artifactId>jib-maven-plugin</artifactId>
  <version>2.8.0</version>
  <configuration>
    <to>
      <image>registry.hub.docker.com/ankit23022/google-jib-image-example</image>
    </to>
  </configuration>
</plugin>

Update settings.xml file which is present in .m2 repositiory

<server>
            <id>registry.hub.docker.com</id>
            <username>my_acccount</username>
            <password>my_password_encrypt_by_maven</password>
        </server>

Now go to terminal and write:-

mvn clean compile jib:build

This command will prepared and push the image to docker HUB

If you make any changes and wish to update and push your docker image to docker hub we'll use:-

Plugins---->jib---->jib:build 


--------------------------------------------------
