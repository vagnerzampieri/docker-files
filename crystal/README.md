sudo docker build -t crystal .

sudo docker run -v /home/user/crystal/shared:/home/marvin/Projects -p 8080:8080 -p 3000:3000 -ti crystal /bin/bash
