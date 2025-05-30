# Tutorial 11 - Deployment

## Reflection on Hello Minikub

1. Compare the application logs before and after you exposed it as a Service. Try to open the app several times while the proxy into the Service is running. What do you see in the logs? Does the number of logs increase each time you open the app?

   > Sebelum aplikasi diekspos sebagai Service, log hanya menunjukkan aktivitas internal dari container karena tidak ada akses dari luar. Setelah aplikasi diekspos sebagai Service dan dibuka melalui browser, jumlah log meningkat setiap kali aplikasi diakses. Ini menunjukkan bahwa setiap permintaan dari klien seperti browser tercatat di log aplikasi.
  
3. Notice that there are two versions of `kubectl get` invocation during this tutorial section. The first does not have any option, while the latter has `-n` option with value set to `kube-system`. What is the purpose of the `-n` option and why did the output not list the pods/services that you explicitly created?

    > Perintah kubectl get tanpa opsi -n hanya menampilkan resource di namespace default, yaitu tempat resource seperti Pod dan Service buatan kita disimpan secara bawaan. Sementara itu, perintah kubectl get -n kube-system menampilkan resource di namespace kube-system, yang digunakan oleh komponen internal Kubernetes. Karena resource yang kita buat tidak berada di kube-system, maka mereka tidak muncul saat menggunakan opsi tersebut.

    ![image](https://github.com/user-attachments/assets/9020f6a4-e19a-423e-8bcd-5c0a7d92f0b7)


## Reflection on Rolling Update & Kubernetes Manifest File

1. What is the difference between Rolling Update and Recreate deployment strategy?

   > Rolling Update adalah strategi default di Kubernetes yang memperbarui Pod satu per satu, sehingga tidak ada downtime karena Pod baru dibuat sebelum Pod lama dihapus. Sementara itu, Recreate akan menghapus semua Pod lama terlebih dahulu, baru kemudian membuat Pod baru. Strategi Recreate berisiko menyebabkan downtime, tetapi bisa berguna jika versi aplikasi baru tidak bisa berjalan berdampingan dengan yang lama.

2. Try deploying the Spring Petclinic REST using Recreate deployment strategy and document your attempt.

    > Untuk mendeploy Spring Petclinic REST menggunakan strategi Recreate, saya akan memodifikasi manifest deployment dengan menambahkan spesifikasi strategy. Pertama, saya akan membuat file deployment.yaml yang menggunakan type: Recreate dalam bagian strategy. Kemudian menjalankan kubectl apply -f deployment.yaml untuk mengaplikasikan konfigurasi tersebut.
   
     ![image](https://github.com/user-attachments/assets/0d77972a-2f70-4e88-90fc-a919c2c6ce23)

   > Saat melakukan update dengan strategi Recreate, yang dapat diamati adalah semua pod akan terminated secara bersamaan, kemudian setelah semua pod lama hilang, pod-pod baru akan mulai dibuat. Selama periode transisi ini, jika kita mengakses aplikasi melalui service, kita akan mendapatkan error atau connection refused karena tidak ada pod yang aktif. Proses ini membutuhkan waktu lebih lama untuk aplikasi menjadi available kembali dibandingkan dengan Rolling Update.

4. Prepare different manifest files for executing Recreate deployment strategy.

    > Untuk eksekusi deployment strategy, saya menyiapkan tiga file terpisah: deployment-recreate.yaml untuk konfigurasi deployment dengan strategi Recreate, service-recreate.yaml untuk mengekspos aplikasi

5. What do you think are the benefits of using Kubernetes manifest files? Recall your experience in deploying the app manually and compare it to your experience when deploying the same app by applying the manifest files (i.e., invoking kubectl apply -f command) to the cluster.

    > Menggunakan manifest file jauh lebih efisien dan terstruktur dibandingkan menjalankan perintah manual satu per satu. Dengan file YAML, saya bisa mendokumentasikan konfigurasi lengkap (seperti image, port, strategy, dan environment), mengelolanya dengan version control seperti Git, dan dengan satu perintah kubectl apply -f, seluruh konfigurasi bisa diterapkan ke cluster. Dibandingkan konfigurasi manual, manifest membuat proses deployment lebih cepat, konsisten, dan mudah diulang di lingkungan lain.
