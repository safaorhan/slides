---
author: "> ssh slides.safaorhan.com -p 4242"
date: ""
paging: "%d / %d"
---

##### MockWebServer ile Gerçekçi ViewModel Testleri

 Safa Orhan

---

##### Safa Orhan

* bilgisayar mühendisi | boun cmpe 17'
* 2013'ten bu yana     | android geliştirici
* 2020'den bu yana     | Konya
* şimdi                | lead android dev @ RTIC Outdoors
* twitter              | `@safaorhanTR`, @safaorhanEN
* youtube              | SafaOrhanTR, Safa Orhan
* başka                | linkedin, medium, github

---

##### MockWebServer ile Gerçekçi ViewModel Testleri

- Test
- ViewModel
- ViewModel Testleri
- Gerçekçi Test
- Gerçekçi ViewModel Testleri
- MockWebServer `<- Birazdan`
- MockWebServer ile Gerçekçi ViewModel Testleri `<- Buradasınız`

---

##### MockWebServer

A scriptable web server for testing HTTP clients

https://github.com/square/okhttp/tree/master/mockwebserver

---

##### Sorun:

Unit testlerde gerçek sunucuya gerçek istekler atamazsınız.

---

##### Sorun:

Unit testlerde gerçek sunucuya gerçek istekler atamazsınız.

------

- Sürekli internetin varlığından emin olamazsınız.
- Sunucunun sürekli açık olacağından emin olamazsınız.
- Bağlantı zamanları çok uzundur.
- Sunucu her zaman aynı sonucu vermez, beklenmediktir.

---

##### Çözüm 0:

Test yazmaktan vazgeçer ve hiçbir şey yokmuş gibi davranırsınız.`*`


------
```kotlin
@Test
fun test() {
    // TODO: Bi ara test yazılacak.
}
```
------

---

##### Çözüm 0:

Test yazmaktan vazgeçer ve hiçbir şey yokmuş gibi davranırsınız.`*`


------
```kotlin
@Test
fun test() {
    // TODO: Bi ara test yazılacak.
}
```
------

`* Bu çözüm mantıklı geldiyse, sunumun geri kalanı sizin için çok sıkıcı olabilir :/` 

---

##### Çözüm 1:

Mock repository kullanırsınız.

------
```kotlin
@Test
fun `given update will succeed, when user clicks save, it should show success`() {

    // Given update will succeed
    coEvery {
        mockRepository.updateUser(USER_UPDATE_REQUEST)
    } returns AsyncResult.Success(UPDATED_USER)

    // When user clicks save
    viewModel.onSaveButtonClick()

    // Should show success 
    assertThat(viewModel.state().successVisible).isTrue
}
```
------

---

##### Çözüm 2:

Fake repository kullanırsınız.

------
```kotlin
@Test
fun `given update will succeed, when user clicks save, it should show success`() {

    // Given update will succeed
    testRepository.updateShouldFail = false

    // When user clicks save
    viewModel.onSaveButtonClick()

    // Should show success
    assertThat(viewModel.state().successVisible).isTrue
}
```
------

---

##### Çözüm 3:

MockWebServer ile gerçek repository kullanırsınız.

------
```kotlin
@Test
fun `given update will succeed, when user clicks save, it should show success`() {

    // Given update will succeed
    server.givenUserUpdate().willSucceed()

    // When user clicks save
    viewModel.onSaveButtonClick()

    // Should show success
    assertThat(viewModel.state().successVisible).isTrue
}
```
------

---

##### Örnek Uygulama

https://github.com/safaorhan/jokes

- Kotlin
- MVVM
- LiveData
- Compose
- Dagger & Hilt
- Coroutines
- Retrofit

------

- MockWebServer
- Hiroaki (https://github.com/JorgeCastilloPrz/hiroaki)
- AssertJ
- Some utils

---

##### Soru Cevap

Sorularınız var mı?

Beni `YouTube` ve `Twitter`'da takip etmeyi unutmayın :)

Dinlediğiniz için teşekkürler!
