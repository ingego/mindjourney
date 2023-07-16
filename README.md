
# Проектирование сервиса 


## User
Логика работы с Пользователями внутри Сервиса
 **  **
```mermaid
---
title: Пользовательская база данных на mysql 
---
classDiagram
    class User
    User : Uuid String
    User : databaseId int 
    User : Password String 
    User: Rules List~int~ 
    User : AppleUuid String?  
    User : GoogleUuid String?  
    User : VkUuid String?
    User : PaymentGateWay int <0,1,2= ZERO, РФ, ЕС>    
    User : RegisterDate DateTime 
    User : IsVerification bool  
    User : RegisterDate DateTime
    User : Ip String
    User : Email String?
    User : Phone String? 
    User : login( email, password)
    User : registration(email, password)
    User : loginWithGoogle( GoogleUuid)
    User : registrationWithGoole(GoogleUuid)
    User : loginWithPhone( phone, password)
    User : registrationWithPhone(phone, password)
    User : loginWithApple( AppleUuid)
    User : registrationWithApple(AppleUuid)
    User : callVerification()
    User : callVerificationEmail ()
    User : checkCode(code)
    User : exit()
    User : removeSession ()
    User : removeAccount()
    
```

```mermaid
---
title: Жизненый цикл User
---
stateDiagram
init: Пользователь создан
unVerification: Пользователь на верификации
verification: пользователь подтвердил email
verificationError:пользователь не прошел проверку
stateCheck : Проверка Пользователя
linkService: Добавление связей
chooseRegion : Выбор сервиса
 errorLink : ошибка привязки
success: Успешная привязка


state stateCheck {
    [*]--> unVerification: enter
unVerification-->verification: отправка на email кода
unVerification-->verificationError: не прошел проверку
verificationError --> unVerification 
verification -->[*] : exit 
}
state linkService {
[*] --> chooseRegion
chooseRegion --> google
chooseRegion --> apple
chooseRegion --> vk
chooseRegion --> phone
vk -->check
apple -->check 
phone --> check
google --> check
check--> errorLink
errorLink --> chooseRegion
check --> success
success --> [*]
}
init --> stateCheck
stateCheck --> linkService
```

## Localization 
** mongoDB ** 

## Settings 
** MySQL **
## FileStorage 
** Alfred **
## Push 
** firebase **
## PayGateway 
** Alfred **
