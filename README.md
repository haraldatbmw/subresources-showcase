# Issue
If I create a quarkus native image, only the files directly inside the META-INF/resources directory are included not the sub-directories and its files.

# Reproduce Bug
1. Start native build in docker: `mvn package -Pnative -Dnative-image.docker-build=true`
2. Build a docker image: `docker build -f src/main/docker/Dockerfile.native -t quarkus/subresource-showcase .`
3. Run the docker image: `docker run -i --rm -p 8080:8080 --name subresource-showcase quarkus/subresource-showcase`
4. Open Browser with URL http://localhost:8080/subdir/index.html and see that an error occurs

# Workaround
1. Open pom.xml and uncomment the additional build arguments (-H:IncludeResources=META-INF/resources/.*)
2. Rebuild, start docker image (see reproduce bug)