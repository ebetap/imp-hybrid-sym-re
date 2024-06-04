### Implementasi tehnik enkripsi hybrid secara simetris untuk react dan express js


Berikut adalah contoh tentang menggabungkan **enkripsi hybrid RSA+AES** dalam aplikasi **React.js** dan **Express.js**:

1. **Instalasi Dependencies**:
    - Pastikan Anda memiliki proyek React.js dan Express.js yang sudah dibuat.
    - Di **React.js**, instalasi **node-forge** untuk mengelola enkripsi RSA dan AES:
      ```bash
      npm install node-forge
      ```
    - Di **Express.js**, Anda dapat menggunakan modul **crypto** bawaan Node.js untuk mengelola enkripsi RSA dan AES.

2. **Generate AES Key di Client (React.js)**:
    - Buat fungsi untuk menghasilkan kunci AES:
      ```javascript
      import forge from 'node-forge';

      export const generateAesKey = () => {
        const aesSalt = forge.random.getBytesSync(16);
        const keyPassPhrase = forge.random.getBytesSync(16);
        const aesKey = forge.pkcs5.pbkdf2(
          keyPassPhrase,
          aesSalt,
          ENCRYPTION_AES_ENC_KEY_OPTIONS.iterations,
          ENCRYPTION_AES_ENC_KEY_OPTIONS.keySize
        );
        return aesKey;
      };
      ```

3. **Generate RSA Key Pair di Server (Express.js)**:
    - Di server Express.js, buat kunci RSA:
      ```javascript
      const crypto = require('crypto');

      const { publicKey, privateKey } = crypto.generateKeyPairSync('rsa', {
        modulusLength: 2048,
        publicKeyEncoding: {
          type: 'spki',
          format: 'pem',
        },
        privateKeyEncoding: {
          type: 'pkcs8',
          format: 'pem',
        },
      });
      ```

4. **Bagikan Kunci Publik RSA ke Client (React.js)**:
    - Kirim kunci publik RSA ke React.js melalui API atau mekanisme lainnya.

5. **Enkripsi Kunci AES dengan Kunci Publik RSA**:
    - Di React.js, enkripsi kunci AES dengan kunci publik RSA:
      ```javascript
      const encryptedAesKey = crypto.publicEncrypt(publicKey, aesKey);
      ```

6. **Enkripsi Data dengan Kunci AES**:
    - Di React.js, enkripsi data yang ingin dikirim:
      ```javascript
      const encryptedData = encryptData(data, aesKey);
      ```

7. **Kirim Data Terenkripsi dan Kunci Terenkripsi ke Server (Express.js)**:
    - Kirim data terenkripsi dan kunci terenkripsi ke server melalui API.

8. **Dekripsi di Server (Express.js)**:
    - Di server, dekripsi kunci AES dengan kunci pribadi RSA:
      ```javascript
      const decryptedAesKey = crypto.privateDecrypt(privateKey, encryptedAesKey);
      ```

9. **Dekripsi Data dengan Kunci AES**:
    - Di server, dekripsi data yang diterima:
      ```javascript
      const decryptedData = decryptData(encryptedData, decryptedAesKey);
      ```

Pastikan untuk mengganti nilai-nilai kunci dan parameter sesuai dengan kebutuhan aplikasi Anda. Semoga membantu! 😊

Source: 6/4/2024
(1) RSA Encryption in Node.js with Code Samples - Plain English. https://plainenglish.io/blog/rsa-encryption-in-nodejs-with-code-samples-86bb829718e0.
(2) RSA Encryption, Decryption and Signing in Node.js (Javascript) - With .... https://www.sohamkamani.com/nodejs/rsa-encryption/.
(3) GitHub - cberthou/aes-gcm-rsa-oaep. https://github.com/cberthou/aes-gcm-rsa-oaep.
(4) Node.js JWE using RSAES-OAEP and AES GCM - Example Code. https://www.example-code.com/nodejs/jwe_rsaes_oaep_aes_gcm.asp.
(5) SocialGouv/aes-gcm-rsa-oaep - GitHub. https://github.com/SocialGouv/aes-gcm-rsa-oaep.
(6) undefined. https://github.com/nkhil/node-crypto/blob/master/src/rsa/create-data-to-encrypt.js.
