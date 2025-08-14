
FROM node:22-alpine

WORKDIR /app

# что копируем, куда копируем
COPY . .

CMD [ "node", "app.js" ]


# IMAGE --->> CONTAINER1, CONTAINER2
# Docker engine - часть докер десктоп, которая скачивает образы, создает образы и т.д.



# Команда для создания образа:
# docker build -t console-log-app .

#  console-log-app - название image
# точка это путь до докерфайла

# Команда для запуска образа
# docker run --rm console-log-app
# docker run console-log-app без rm у вас останется конейнер на компьютере

# При запуске образа на компьютере появляется контейнер - 
# конкретная инстанция/реализация образа

