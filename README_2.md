
# Домашние задания по модулю  «Отказоустойчивость»

В этом репозитории расположены ваши домашние задания к каждой лекции. 

Обязательны к выполнению задачи без звездочек. Их нужно выполнить, чтобы получить зачёт.

Задачи со звёздочкой (*) — дополнительные задачи или задачи повышенной сложности. Их выполнять не обязательно, но они помогут вам глубже понять тему.

Любые вопросы по решению задач задавайте в чате учебной группы. Ссылку вы найдёте в письме на вашей электронной почте.
=======
# Домашнее задание к занятию "Отказоустойчивость в облаке" - Лапшов Сергей
=======
### Задание 1

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
terraform {
  required_providers {
    yandex = {
      source = "yandex-cloud/yandex"
    }
  }
}

provider "yandex" {
  token     = "y0_AgAEA7qi-ckDAATuwQAAAAD5TFt5AAB37bbXylpPpJVzBYc7tTbGodRPLA"
  cloud_id  = "b1ga6qkq58gl6ok8unrq"
  folder_id = "b1glic22aocn4v5kcfj3"
  zone      = "ru-central1-a"
}

resource "yandex_vpc_network" "test" {
  name = "test"
}

resource "yandex_vpc_subnet" "subnet-1" {
  name           = "subnet1"
  zone           = "ru-central1-a"
  network_id     = yandex_vpc_network.test.id
  v4_cidr_blocks = ["192.168.10.0/24"]
}

output "subnet_id" {
  value = yandex_vpc_subnet.subnet-1.id
}

resource "yandex_compute_instance" "vm" {
  count = 2
  name  = "terraform${count.index + 1}"

  resources {
    cores  = 2
    memory = 2
  }

  boot_disk {
    initialize_params {
      image_id = "fd87kbts7j40q5b9rpjr"
    }
  }

  network_interface {
    subnet_id = yandex_vpc_subnet.subnet-1.id
    nat       = true
  }

  metadata = {
    user-data = "${file("./meta.txt")}"
  }

  provisioner "file" {
    source      = "install_nginx.sh"
    destination = "/tmp/install_nginx.sh"
  }

  provisioner "remote-exec" {
    inline = [
      "chmod +x /tmp/install_nginx.sh",
      "/tmp/install_nginx.sh"
    ]
  }
}

resource "yandex_lb_target_group" "foo" {
  name      = "my-target-group"
  region_id = "ru-central1"

  target {
    subnet_id = yandex_vpc_subnet.subnet-1.id
    address   = yandex_compute_instance.vm[0].network_interface[0].ip_address
  }

  target {
    subnet_id = yandex_vpc_subnet.subnet-1.id
    address   = yandex_compute_instance.vm[1].network_interface[0].ip_address
  }
}

resource "yandex_lb_network_load_balancer" "test-1" {
  name = "test-1"

  listener {
    name = "my-lis"
    port = 80
    external_address_spec {
      ip_version = "ipv4"
    }
  }

  attached_target_group {
    target_group_id = yandex_lb_target_group.foo.id

    healthcheck {
      name = "http"
      http_options {
        port = 80
        path = "/"
      }
    }
  }
}

output "internal_ip_addresses" {
  value = yandex_compute_instance.vm[*].network_interface[0].ip_address
}

output "external_ip_addresses" {
  value = yandex_compute_instance.vm[*].network_interface[0].nat_ip_address
}
```

`При необходимости прикрепитe сюда скриншоты
![Скриншот статуса балансировщика и целевой группы](https://github.com/DavyRoy/sflt-homeworks/blob/main/Снимок%20экрана%20от%202024-03-20%2011-26-14.png)
![Скриншот страницы, которая открылась при запросе IP-адреса балансировщика.](https://github.com/DavyRoy/sflt-homeworks/blob/main/Снимок%20экрана%20от%202024-03-20%2011-31-12.png)
![Скриншот страницы, которая открылась при запросе IP-адреса балансировщика.](https://github.com/DavyRoy/sflt-homeworks/blob/main/Снимок%20экрана%20от%202024-03-20%2011-32-40.png)

---

### Задание 2

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота 2](ссылка на скриншот 2)`


---

### Задание 3

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`

### Задание 4

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`
>>>>>>> 73d1e2b (commit)
