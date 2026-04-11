

<img width="1216" height="544" alt="image" src="https://github.com/user-attachments/assets/47b1c3c3-9ac0-43c8-a086-2baa3df2b38f" />
<img width="1227" height="578" alt="image" src="https://github.com/user-attachments/assets/62a196a1-149d-4a86-85dd-e46c54bc2c02" />
<img width="974" height="482" alt="image" src="https://github.com/user-attachments/assets/a06870be-9200-4cc5-8916-729f36b37104" />


<img width="1196" height="466" alt="image" src="https://github.com/user-attachments/assets/2953e0b8-f33d-4707-873f-acf7ba733372" />

<img width="659" height="508" alt="image" src="https://github.com/user-attachments/assets/67a95ed0-639d-4d6a-a696-85e40028ac89" />


```
FROM node:18-alpine

ENV MONGO_DB_USERNAME=admin \
    MONGO_DB_PWD=password

RUN mkdir -p /home/app

COPY . /home/app

# # set default dir so that next commands executes in /home/app dir
# WORKDIR /home/app

# will execute npm install in /home/app because of WORKDIR
#RUN npm install

# no need for /home/app/server.js because of WORKDIR
CMD ["node", "/home/app/server.js"]
```
