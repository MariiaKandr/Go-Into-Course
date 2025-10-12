## Язык Go (Golang)

Компилируемый язык для разработки серверных приложений, микросервисов, сетевых инструментов и утилит.

<img width="1576" height="890" alt="IMG_3613" src="https://github.com/user-attachments/assets/9b1cfe64-8d3c-4205-b877-df164f229c7f" />


## Ключевые особенности

* Параллелизм: лёгкие потоки — **goroutine** и **каналы**.
* Статическая типизация + простая семантика.
* Встроенный сборщик мусора.
* Сильная стандартная библиотека (сеть, HTTP, кодирование, тестирование).
* Инструменты: `go fmt`, `go test`, `go build`, `go vet`, `pprof`.

## Типичные области применения

* Backend / API-сервисы
* Микросервисы и облачные приложения
* Сетевые/CLI-инструменты и утилиты DevOps
* Системы с высокими требованиями к параллелизму и производительности

## Установка
Ссылка на официальный сайт: https://go.dev 

### Проверка перед началом

В терминале выполните:

```
go version
```

Если версия не отображается — Go не установлен или не в PATH.

### Windows

1. Скачайте установщик `.msi` с официального сайта (go.dev) и запустите.
2. Перезагрузите терминал (или ПК) и проверьте `go version`.

### macOS

Вариант A — официальным pkg-пакетом с go.dev: скачайте и установите `.pkg`.
Вариант B — через Homebrew:

```
brew install go
```

Проверьте: `go version`.

### Linux (ручная установка)

1. Скачайте архив `goX.Y.Z.linux-amd64.tar.gz` с официального сайта.
2. Распакуйте в `/usr/local`:

```
sudo tar -C /usr/local -xzf goX.Y.Z.linux-amd64.tar.gz
```

3. Добавьте в PATH (например в `~/.profile` или `~/.bashrc`):

```
export PATH=$PATH:/usr/local/go/bin
```

4. Перезапустите терминал и проверьте `go version`.

## Настройка VS Code для разработки на Go
Полная инструкция от Microsoft: https://learn.microsoft.com/ru-ru/azure/developer/go/configure-visual-studio-code 
1. Установите Visual Studio Code.
2. Откройте VS Code → Extensions (Ctrl+Shift+X) → найдите и установите расширение **Go** (от команды Go).
     <img width="1139" height="647" alt="IMG_3615" src="https://github.com/user-attachments/assets/14a541c7-0dec-4321-a57d-a302e88dcb5f" />
3. Откройте папку с проектом (File → Open Folder).
4. При первом открытии `.go` файлов расширение предложит установить дополнительные инструменты (gopls, dlv и пр.). Разрешите установку.
Рекомендуемые команды:

   * Форматирование: `Shift+Alt+F` (или `go fmt`).
   * Запуск тестов: `go test ./...`.
   * Отладка: используйте `Delve` (инструмент `dlv`) через конфигурацию отладчика в `.vscode/launch.json`.

## Минимальный проект и запуск

Создайте файл `main.go`:

```go
package main
import "fmt"
func main() {
    fmt.Println("Hello, Go!")
}
```

Сборка и запуск:

```
go run main.go
```

## Онлайн-инструмент 

* Go Playground: [https://go.dev/play](https://go.dev/play)

