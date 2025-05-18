# Домашнее задание к занятию «Введение в Terraform»
## Задача 0
![image](https://github.com/EremeevAN/ter-home01/blob/main/images/1.png)
## Задание 1
2. personal.auto.tfvars
3. "result": "fEhRH9zTqUbb8SXb"
4. выполняем команду "terraform validate" получаем ошибки:
![image](https://github.com/EremeevAN/ter-home01/blob/main/images/2.png)
Проверяем:
было так:
resource "docker_image" {
  name         = "nginx:latest"
  keep_locally = true
}

resource "docker_container" "1nginx" {
  image = docker_image.nginx.image_id
  name  = "example_${random_password.random_string_FAKE.resulT}"

  ports {
    internal = 80
    external = 9090
  }
}
стало так:
resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = true
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = "example_${random_password.random_string.result}"
  Ошибки:
   1. в строке "resource "docker_image" {" пропущено имя "nginx"
   2. в строке "resource "docker_container" "1nginx" {" лишний символ 1
   3. в строке "name  = "example_${random_password.random_string_FAKE.resulT}"" вместо "FAKE.resulT" должно быть "result"
5. ![image](https://github.com/EremeevAN/ter-home01/blob/main/images/3.png)
6.  
name  = "example_${random_password.random_string.result}" меняем на name  = "hello_world"
Получаем:
![image](https://github.com/EremeevAN/ter-home01/blob/main/images/4.png)
опасность применения ключа -auto-approve:
Ключ -auto-approve автоматически без вмешательства пользователя применяет изменения, есть вероятность потери данных
7. выполним команду "terraform destroy". Cодержимое файла terraform.tfstate 
{
  "version": 4,
  "terraform_version": "1.11.0",
  "serial": 11,
  "lineage": "30b59e33-557a-b0cc-8232-15b2e6310886",
  "outputs": {},
  "resources": [],
  "check_results": null
}
8. keep_locally = true
![image](https://github.com/EremeevAN/ter-home01/blob/main/images/5.png)