Environtment de
ANDROID_HOME
JAVA_HOME
GRADLE_HOME (gradle indirilip c:\ açýlýrsa bu opsiyo eklenebilir)

tanýmlamalarý yapýlýr.
----------------------------------------------
D:\android\sdk\platform-tools
D:\android\sdk\tools
%JAVA_HOME%;%JAVA_HOME%\bin;%GRADLE_HOME%;

PATH e eklenir
--------------   ANDROID TELEFONDAN UYGULAMA TESTÝ YAPARKEN ---------------------------------------
ANDROID TELEFONDAN UYGULAMA TESTÝ YAPARKEN
Android Geliþtiriciyi açmak için telefon hakkýnda kýsmýnda, 
Derleme Numarasýna 7 kez arka arkaya basýlýr.

----------------- AVD seçimi ----------------------------------------------------------------------

cordova emulate --target=avdismi [android]
seçilmez ise cordova minsdk 14 olduðunda SDK da sý en azýndan yüklenmeli ve avd tanýmlanmalý

----------------- *********** USB den android cihaz baðlýysa ********** ----------------------------

Chrome dan doðrudan debug için
Inscpect edildiðinde, cordova da build edildikten sonra
run diyerek USB olarak baðlanan android debug edilebilir.

chrome://inspect/#devices

------------------ SPLASH SCREEN PROBLEMÝ ----------------------------------------------------------

Splash screen ve icon da çýkan sorunlar, adnroid platformu kaldýrýlýp 
yeniden kurulduðunda ortadan kalkar.
======
splashscreen ya da icon da herhangi bir hata varsa
rma (cordova plastform rm android) ile platform kaldýrýlýr
adda (cordova plastform add android) ile platform eklenerek düzeltilir...(Bug!)
clean iþlemi splashscreen/icon da düzeltme yapmamaktadýr.

---------------------------------------------------------------------------------------------------
			 ANDROID DEVELOPMENT STEPS
----------------------------------------------------------------------------------------------------
release 
iþlendikten sonra
KEY BUILD (APK BUILD)

Bat dosyalarý açýklamasý:
--------------------------
%1 ===> %1.keystore dosyasýna verilecek isim %1 ile girilir
Ayný isimde olsun dediðimiz için hepsinde ayný ismi kullandýk.
Farklý isim kullanýlacak ise, bat dosyasýnda düzenleme yapýlýr %1 %2 gibi..
Bu durumda, örneðin key.bat çalýþtýrýlýrken key xxx yyy gibi girilmeli.

key %1 (keystore dosyas adý) genelde program adý
==> keytool -genkey -v -keystore %1.keystore -alias %1 -keyalg RSA -keysize 2048 -validity 10000

sign %1 (yukarýda keystore ye verilen isim ayný)
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore %1.keystore platforms/android/build/outputs/apk/android-release-unsigned.apk %1

zip  %1 (yukarýdaki isimle ayný artýk apk dosya ismidir)
zipalign -v 4 platforms/android/build/outputs/apk/android-release-unsigned.apk platforms/android/build/outputs/apk/%1.apk

þeklindedir.

vrfy %1 (yukarýdaki isimle ile ayný) sign kontrol (jar verified olmalý)
----------------------------------------------------------------------------------------------------
