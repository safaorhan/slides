---
author: "> ssh devfest.safaorhan.com -p 4242"
date: ""
paging: ""
---

##### MockWebServer ile Gerçekçi ViewModel Testleri

 Safa Orhan

---

##### Safa Orhan

- Bilgisayar mühendisiyim. (Boun CmpE)

---

##### Safa Orhan

- Bilgisayar mühendisiyim. (Boun CmpE)
- 8+ senedir Android geliştiriyorum.

---

##### Safa Orhan

- Bilgisayar mühendisiyim. (Boun CmpE)
- 8+ senedir Android geliştiriyorum.
- Şu anda bir Amerikan şirketinde takım lideri olarak çalışıyorum.

---

##### MockWebServer

A scriptable web server for testing HTTP clients

https://github.com/square/okhttp/tree/master/mockwebserver

---

##### Sorun:

Testlerde gerçek sunucuya gerçek istekler atamazsınız.

---

##### Çözüm 0:

Test yazmaktan vazgeçer ve hiçbir şey yokmuş gibi davranırsınız.


------
```kotlin
@Test
fun test() {
    // TODO: Bi ara test yazılacak.
}
```
------

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

