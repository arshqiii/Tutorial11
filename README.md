# Tutorial 11 - Deployment

1. Compare the application logs before and after you exposed it as a Service. Try to open the app several times while the proxy into the Service is running. What do you see in the logs? Does the number of logs increase each time you open the app?
> Sebelum aplikasi diekspos sebagai Service, log hanya menunjukkan aktivitas internal dari container karena tidak ada akses dari luar. Setelah aplikasi diekspos sebagai Service dan dibuka melalui browser, jumlah log meningkat setiap kali aplikasi diakses. Ini menunjukkan bahwa setiap permintaan dari klien seperti browser tercatat di log aplikasi.
  
2. Notice that there are two versions of `kubectl get` invocation during this tutorial section. The first does not have any option, while the latter has `-n` option with value set to `kube-system`. What is the purpose of the `-n` option and why did the output not list the pods/services that you explicitly created?
> Perintah kubectl get tanpa opsi -n hanya menampilkan resource di namespace default, yaitu tempat resource seperti Pod dan Service buatan kita disimpan secara bawaan. Sementara itu, perintah kubectl get -n kube-system menampilkan resource di namespace kube-system, yang digunakan oleh komponen internal Kubernetes. Karena resource yang kita buat tidak berada di kube-system, maka mereka tidak muncul saat menggunakan opsi tersebut.
