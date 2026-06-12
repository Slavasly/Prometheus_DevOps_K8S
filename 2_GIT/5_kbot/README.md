# kbot
2.5. Coding Session «Telebot»
https://youtu.be/cSky-GIwjek 
00:00 Тема лекції Telebot Framework
00:39 Початковий код
00:48 Пакети та import у golang
import (
	"fmt"

	"github.com/spf13/cobra"
	telebot "gopkg.in/telebot.v3"
)
01:30 Додаємо змінну TeleToken
var (
	// TeleToken bot
	TeleToken = os.Getenv("TELE_TOKEN")
)
02:00 Додаємо код функції run
	Run: func(cmd *cobra.Command, args []string) {
		fmt.Printf("kbot %s started", appVersion)
		kbot, err := telebot.NewBot(telebot.Settings{
			URL:	"",
			Token:	TeleToken,
			Poller: &telebot.LongPoller{Timeout: 10 * time.Second},
		})
	},
02:55 Обробник помилок та handler
		kbot.Handle(telebot.OnText, func(m telebot.Context) error {
			log.Print(m.Message().Payload, m.Text())
			return err
		})
		
		kbot.Start()

03:44 Збірка проєкту go build
gofmt -s -w ./
$ go get
go: downloading gopkg.in/telebot.v3 v3.1.4
go: added gopkg.in/telebot.v3 v3.1.4
$ go build -ldflags "-X="github.com/slavasly/kbot/cmd.appVersion=v1.0.1
cmd/kbot.go:33:39: undefined: telebot.settings
cmd/kbot.go:40:8: undefined: log.FatalI (Add log to import)
cmd/kbot.go:45:27: undefined: Payload (fix typing m.Message().Payload)

# виправляємо помилки в коді та повторюємо команди
gofmt -s -w ./
go build -ldflags "-X="github.com/slavasly/kbot/cmd.appVersion=v1.0.1
./kbot
 
#Додаємо аліас до команди kbot                        
var kbotCmd = &cobra.Command{
	Use:     "kbot",
    	Aliases: []string{"start"},

# Компілюємо код та запускаємо ще раз:
$ go build -ldflags "-X="github.com/slavasly/kbot/cmd.appVersion=v1.0.1
$ ./kbot start

04:54 Створюємо телеграм бота та отримуємо токен
Підготуємо бота. Відкриємо телеграм, знайдемо BotFather та створимо нового бота командою /newbot
Скопіюємо API token від нового бота

$ read -s TELE_TOKEN (click Enter)
 Ctr+V click Enter
echo $TELE_TOKEN
0123456789:ARFGGy73tD

05:50 Перевіряємо працездатність бота
./kbot start
kbot v1.0.1 started
Click /start in Telegram bot and find /start in console
2026/04/17 20:32:26 /start

Send message from Telegram bot “Hello”
In console we saw 2026/04/17 20:32:37 hello

06:15 Розширюємо функціонал бота - Додамо трохи коду до хендлеру щоб забезпечити двосторонній зв'язок.

kbot.Handle(telebot.OnText, func(m telebot.Context) error {
            log.Print(m.Message().Payload, m.Text())
            payload := m.Message().Payload

            switch payload {
            case "hello":
                err = m.Send(fmt.Sprintf("Hello I'm Kbot %s!", appVersion))
            }

            return err

06:45 Перевірка працездатності бота
$ go build -ldflags "-X="github.com/slavasly/kbot/cmd.appVersion=v1.0.2
 $ ./kbot start
kbot v1.0.2 started 2026/04/17 20:22:18 /start
2026/04/17 20:22:36 /start
2026/04/17 20:23:00 /start hello - we saw in telegram the message Hello I'm Kbot v1.0.2!
