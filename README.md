# Регистрация и Настройка Git на Mac

Эта инструкция поможет вам зарегистрироваться на GitHub, установить Git и настроить его на Mac. Следуйте шагам ниже:

## Шаг 1: Регистрация на GitHub

1. Перейдите на сайт [GitHub](https://github.com/).
2. Нажмите на кнопку **Sign up** в правом верхнем углу.
3. Заполните форму регистрации:
    - Введите ваш email.
    - Создайте и введите пароль.
    - Придумайте и введите имя пользователя.
4. Нажмите **Create account**.
5. Следуйте инструкциям на экране для завершения регистрации (проверка email и т.д.).

## Шаг 2: Установка Git

### С помощью Homebrew

1. Установите Homebrew, если он еще не установлен. Откройте Terminal и выполните следующую команду:
    ```sh
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```
2. Установите Git с помощью Homebrew:
    ```sh
    brew install git
    ```

### С помощью Git Installer

1. Перейдите на [сайт Git](https://git-scm.com/download/mac).
2. Скачайте последнюю версию Git.
3. Откройте загруженный файл и следуйте инструкциям установщика.

## Шаг 3: Проверка установки

После установки откройте Terminal и выполните следующую команду, чтобы проверить установленную версию Git:
```sh
git --version
```
Вы должны увидеть что-то вроде:
```
git version 2.x.x
```

## Шаг 4: Настройка Git

1. Откройте Terminal.
2. Настройте ваше имя пользователя:
    ```sh
    git config --global user.name "Ваше Имя"
    ```
3. Настройте ваш email:
    ```sh
    git config --global user.email "ваш.email@example.com"
    ```
4. Проверьте настройки, выполнив:
    ```sh
    git config --list
    ```

## Шаг 5: Генерация SSH ключа (опционально, но рекомендуется)

1. Проверьте, есть ли у вас уже SSH ключи:
    ```sh
    ls -al ~/.ssh
    ```
2. Если ключей нет, создайте новый:
    ```sh
    ssh-keygen -t ed25519 -C "ваш.email@example.com"
    ```
   Следуйте инструкциям на экране, оставляя настройки по умолчанию.

3. Добавьте SSH ключ в ssh-agent:
    ```sh
    eval "$(ssh-agent -s)"
    ssh-add -K ~/.ssh/id_ed25519
    ```
4. Скопируйте SSH ключ в буфер обмена:
    ```sh
    pbcopy < ~/.ssh/id_ed25519.pub
    ```
5. Перейдите в настройки вашего аккаунта на GitHub:
    - Нажмите на ваш аватар в правом верхнем углу и выберите **Settings**.
    - В меню слева выберите **SSH and GPG keys**.
    - Нажмите **New SSH key**, вставьте ключ из буфера обмена и нажмите **Add SSH key**.

## Шаг 6: Клонирование репозитория

1. Найдите репозиторий на GitHub, который хотите клонировать.
2. Нажмите кнопку **Code** и скопируйте SSH URL.
3. В Terminal выполните команду:
    ```sh
    git clone git@github.com:username/repository.git
    ```

Теперь вы успешно настроили Git на вашем Mac и можете начинать работу с репозиториями!
