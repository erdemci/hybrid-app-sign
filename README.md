Environtment de
ANDROID_HOME
JAVA_HOME
GRADLE_HOME (gradle indirilip c:\ a��l�rsa bu opsiyo eklenebilir)

tan�mlamalar� yap�l�r.
----------------------------------------------
D:\android\sdk\platform-tools
D:\android\sdk\tools
%JAVA_HOME%;%JAVA_HOME%\bin;%GRADLE_HOME%;

PATH e eklenir
--------------   ANDROID TELEFONDAN UYGULAMA TEST� YAPARKEN ---------------------------------------
ANDROID TELEFONDAN UYGULAMA TEST� YAPARKEN
Android Geli�tiriciyi a�mak i�in telefon hakk�nda k�sm�nda, 
Derleme Numaras�na 7 kez arka arkaya bas�l�r.

----------------- AVD se�imi ----------------------------------------------------------------------

cordova emulate --target=avdismi [android]
se�ilmez ise cordova minsdk 14 oldu�unda SDK da s� en az�ndan y�klenmeli ve avd tan�mlanmal�

----------------- *********** USB den android cihaz ba�l�ysa ********** ----------------------------

Chrome dan do�rudan debug i�in
Inscpect edildi�inde, cordova da build edildikten sonra
run diyerek USB olarak ba�lanan android debug edilebilir.

chrome://inspect/#devices

------------------ SPLASH SCREEN PROBLEM� ----------------------------------------------------------

Splash screen ve icon da ��kan sorunlar, adnroid platformu kald�r�l�p 
yeniden kuruldu�unda ortadan kalkar.
======
splashscreen ya da icon da herhangi bir hata varsa
rma (cordova plastform rm android) ile platform kald�r�l�r
adda (cordova plastform add android) ile platform eklenerek d�zeltilir...(Bug!)
clean i�lemi splashscreen/icon da d�zeltme yapmamaktad�r.

---------------------------------------------------------------------------------------------------
			 ANDROID DEVELOPMENT STEPS
----------------------------------------------------------------------------------------------------
release 
i�lendikten sonra
KEY BUILD (APK BUILD)

Bat dosyalar� a��klamas�:
--------------------------
%1 ===> %1.keystore dosyas�na verilecek isim %1 ile girilir
Ayn� isimde olsun dedi�imiz i�in hepsinde ayn� ismi kulland�k.
Farkl� isim kullan�lacak ise, bat dosyas�nda d�zenleme yap�l�r %1 %2 gibi..
Bu durumda, �rne�in key.bat �al��t�r�l�rken key xxx yyy gibi girilmeli.

key %1 (keystore dosyas ad�) genelde program ad�
==> keytool -genkey -v -keystore %1.keystore -alias %1 -keyalg RSA -keysize 2048 -validity 10000

sign %1 (yukar�da keystore ye verilen isim ayn�)
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore %1.keystore platforms/android/build/outputs/apk/android-release-unsigned.apk %1

zip  %1 (yukar�daki isimle ayn� art�k apk dosya ismidir)
zipalign -v 4 platforms/android/build/outputs/apk/android-release-unsigned.apk platforms/android/build/outputs/apk/%1.apk

�eklindedir.

vrfy %1 (yukar�daki isimle ile ayn�) sign kontrol (jar verified olmal�)
----------------------------------------------------------------------------------------------------
