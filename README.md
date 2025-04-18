# gitlab
### Задание 1
Что нужно сделать:

Разверните GitLab локально, используя Vagrantfile и инструкцию, описанные в этом репозитории.

Создайте новый проект и пустой репозиторий в нём.

Зарегистрируйте gitlab-runner для этого проекта и запустите его в режиме Docker.

Раннер можно регистрировать и запускать на той же виртуальной машине, на которой запущен GitLab.

В качестве ответа в репозиторий шаблона с решением добавьте скриншоты с настройками раннера в проекте.

Решение 1


![Снимок 199](https://github.com/user-attachments/assets/355d8e7c-8fc6-4b57-bb98-be42ef576bda)
![Снимок 200](https://github.com/user-attachments/assets/c531e75c-8965-4807-a81b-58131f508bb3)
![Снимок 203](https://github.com/user-attachments/assets/d888eb83-bfd9-43e2-ab4b-e1fcb21c38e9)


### Задание 2
Что нужно сделать:

Запушьте репозиторий на GitLab, изменив origin. Это изучалось на занятии по Git.

Создайте .gitlab-ci.yml, описав в нём все необходимые, на ваш взгляд, этапы.

В качестве ответа в шаблон с решением добавьте:

файл gitlab-ci.yml для своего проекта или вставьте код в соответствующее поле в шаблоне;
скриншоты с успешно собранными сборками.

Решение 2
Содержимое gitlab-ci.yml
 ```
stages:
  - test
  - static-analysis
  - build

test:
  stage: test
  image: golang:1.16
  script: 
   - go test .

static-analysis:
 stage: test
 image:
  name: sonarsource/sonar-scanner-cli
  entrypoint: [""]
 variables:
 script:
  - sonar-scanner -Dsonar.projectKey=checkeray -Dsonar.sources=. -Dsonar.host.url=http://51.250.102.151:9000 -Dsonar.login=sqp_d7488143f45cd61c4d8de98b972ddf49ab52f910

build:
  stage: build
  image: docker:latest
  script:
   - docker build . --tag gitlab-ci:latest
 ```
Скриншоты:

![Снимок 201](https://github.com/user-attachments/assets/b6cfe613-f3c6-46ae-98b8-b12e0ee5a3ad)
![Снимок 202](https://github.com/user-attachments/assets/943ca531-fb46-407e-bd49-0dc11ffdf1a9)
