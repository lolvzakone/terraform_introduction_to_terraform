# terraform_introduction_to_terraform
## Задача 1
### Задача 3.2
Изучите файл .gitignore. В каком terraform-файле, согласно этому .gitignore, допустимо сохранить личную, секретную информацию?(логины,пароли,ключи,токены итд)
#### Ответ:
personal.auto.tfvars , данный файл подходит для хранения чувствительных данных т.к. формат файла .tfvars используется для значения переменных , которые используются в конфигурационных файлах Тераформа.
 также не попадут пароли из файлов с расширением .tfstate
### Задача 3.3
Выполните код проекта. Найдите в state-файле секретное содержимое созданного ресурса random_password, пришлите в качестве ответа конкретный ключ и его значение.
#### Ответ:
"result": "vWfm8O92pX5zVNEV"
### Задача 3.5
Выполните код. В качестве ответа приложите: исправленный фрагмент кода и вывод команды docker ps.
#### Ответ:

resource "docker_image""my_1st_resource" {
  name         = "nginx:latest"
  keep_locally = true
}

resource "docker_container" "nginx" {
  image = docker_image.my_1st_resource.image_id
  name  = "example_${random_password.random_string.result}"

  ports {
    internal = 80
    external = 9090
  }
}


![image](https://github.com/user-attachments/assets/3319c271-35bd-4811-8bb0-e397db4573b9)
### Задача 3.6
Замените имя docker-контейнера в блоке кода на hello_world. Не перепутайте имя контейнера и имя образа. Мы всё ещё продолжаем использовать name = "nginx:latest". Выполните команду terraform apply -auto-approve. Объясните своими словами, в чём может быть опасность применения ключа -auto-approve. Догадайтесь или нагуглите зачем может пригодиться данный ключ? В качестве ответа дополнительно приложите вывод команды docker ps.
#### Ответ:
ключ -auto-approve используется для  выполнения кода без  подтверждений. Может быть опасен если  тераформ будет выполнять код который меняет или удаляет  какие то компоненты. Данный ключ нужен если код уже проверен и   можно исключить ручной ввод подтверждения.
![image](https://github.com/user-attachments/assets/8c33b14e-1e1a-4c4f-a39a-c46102a88105)


### Задача 3.7
Уничтожьте созданные ресурсы с помощью terraform. Убедитесь, что все ресурсы удалены. Приложите содержимое файла terraform.tfstate.
#### Ответ:
ivanit@vbox:/home/ivanit/Ter/ter-homeworks-main/01/src# cat terraform.tfstate
{
  "version": 4,
  "terraform_version": "1.9.8",
  "serial": 16,
  "lineage": "e84a61ca-b46f-79a3-4a2b-bff323b50d0d",
  "outputs": {},
  "resources": [],
  "check_results": null
}

### Задача 3.8
Объясните, почему при этом не был удалён docker-образ nginx:latest. Ответ ОБЯЗАТЕЛЬНО НАЙДИТЕ В ПРЕДОСТАВЛЕННОМ КОДЕ, а затем ОБЯЗАТЕЛЬНО ПОДКРЕПИТЕ строчкой из документации terraform провайдера docker. (ищите в классификаторе resource docker_image )
#### Ответ:
resource "docker_image""my_1st_resource" {
  name         = "nginx:latest"
  keep_locally = true
keep_locally (Boolean) If true, then the Docker image won't be deleted on destroy operation. If this is false, it will delete the image from the docker local storage on destroy operation.
