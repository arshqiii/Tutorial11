# Tutorial 11 - Deployment

## Reflection on Hello Minikub

1. Compare the application logs before and after you exposed it as a Service. Try to open the app several times while the proxy into the Service is running. What do you see in the logs? Does the number of logs increase each time you open the app?
  > Sebelum aplikasi diekspos sebagai Service, log hanya menunjukkan aktivitas internal dari container karena tidak ada akses dari luar. Setelah aplikasi diekspos sebagai Service dan dibuka melalui browser, jumlah log meningkat setiap kali aplikasi diakses. Ini menunjukkan bahwa setiap permintaan dari klien seperti browser tercatat di log aplikasi.
  
2. Notice that there are two versions of `kubectl get` invocation during this tutorial section. The first does not have any option, while the latter has `-n` option with value set to `kube-system`. What is the purpose of the `-n` option and why did the output not list the pods/services that you explicitly created?
  > Perintah kubectl get tanpa opsi -n hanya menampilkan resource di namespace default, yaitu tempat resource seperti Pod dan Service buatan kita disimpan secara bawaan. Sementara itu, perintah kubectl get -n kube-system menampilkan resource di namespace kube-system, yang digunakan oleh komponen internal Kubernetes. Karena resource yang kita buat tidak berada di kube-system, maka mereka tidak muncul saat menggunakan opsi tersebut.

## Reflection on Rolling Update & Kubernetes Manifest File

1. What is the difference between Rolling Update and Recreate deployment strategy?

2. Try deploying the Spring Petclinic REST using Recreate deployment strategy and document your attempt.

3. Prepare different manifest files for executing Recreate deployment strategy.

4. What do you think are the benefits of using Kubernetes manifest files? Recall your experience in deploying the app manually and compare it to your experience when deploying the same app by applying the manifest files (i.e., invoking kubectl apply -f command) to the cluster.
