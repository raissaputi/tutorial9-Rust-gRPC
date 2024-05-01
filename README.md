# Reflection

1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?

    * Unary gRPC adalah metode komunikasi yang cocok untuk interaksi antara klien dan server di mana klien mengirimkan satu permintaan ke server dan menunggu satu respons. Metode ini ideal untuk kasus di mana klien hanya membutuhkan data atau tindakan tunggal dari server.

    * Server streaming gRPC memungkinkan server untuk mengirimkan serangkaian respons kepada klien dalam bentuk aliran data. Metode ini berguna ketika server perlu mengirimkan sejumlah besar data atau aliran pembaruan terus-menerus kepada klien.

    * Bidirectional streaming gRPC adalah pola komunikasi di mana baik klien maupun server dapat mengirimkan beberapa pesan satu sama lain dalam aliran yang kontinu. Ini memungkinkan komunikasi dua arah secara real-time antara klien dan server. Pola ini umumnya digunakan dalam skenario di mana ada kebutuhan untuk komunikasi interaktif yang berkelanjutan.

2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?

    Implementasi gRPC dalam Rust memerlukan pertimbangan keamanan dalam beberapa aspek. Untuk otentikasi dan otorisasi, perlu pastikan bahwa klien dan server saling memverifikasi identitasnya menggunakan metode seperti token OAuth atau JSON Web Tokens (JWT). Perlu dipastikan bahwa hanya klien yang memiliki izin yang sesuai yang dapat mengakses sumber daya atau operasi tertentu. Kemudian untuk enkripsi data, dapat dilakukan dengan menggunakan Transport Layer Security (TLS), untuk melindungi data yang dikirim antara klien dan server dari serangan peretas.

3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?

    Dalam menghadapi bidirectional streaming gRPC dalam Rust, terutama dalam skenario aplikasi chat, tantangan-tantangan utama termasuk pengelolaan memori yang cermat untuk menghindari kebocoran memori, implementasi keamanan data seperti enkripsi dan otentikasi untuk melindungi pesan pribadi, manajemen concurrency agar pesan-pesan dapat ditangani dengan benar, *error-handling* yang baik untuk mengatasi situasi yang tidak terduga, dan manajemen koneksi yang efisien untuk memastikan kelancaran komunikasi antara klien dan server.

4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?

    Advantage:
    
    * Integrasi dengan Tokio: ReceiverStream 

    * Fleksibel. Dengan ReceiverStream, pengelolaan aliran data dari channel mpsc dalam Rust jadi mudah, memungkinkan pemrosesan pesan secara asinkronus dan responsif.

    Disadvantage:

    * ReceiverStream mungkin memiliki keterbatasan dalam hal fungsionalitas bawaan dibandingkan dengan solusi streaming lainnya.

    * Meskipun mudah digunakan, penggunaan ReceiverStream juga memerlukan manajemen channel mpsc yang cermat untuk menghindari kemungkinan kebocoran memori atau deadlock.

5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?

    Pertama, memisahkan logika bisnis dari implementasi gRPC sendiri memungkinkan independensi tanpa terikat pada infrastruktur spesifik. Kedua, menggunakan Protobuf untuk mendefinisikan layanan memperjelas kontrak layanan yang dapat diimplementasikan secara independen, memfasilitasi integrasi dan perubahan dalam proyek. Ketiga, memanfaatkan Traits dalam Rust memungkinkan pembuatan abstraksi yang solid antara layanan dan implementasi konkretnya, memisahkan logika bisnis dari infrastruktur gRPC dan memudahkan pengujian dan perubahan.

6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?

    1. Error Handrling untuk mengatasi kesalahan dengan baik jika ada masalah saat proses pembayaran. 

    2. Validasi data pembayaran yang masuk benar dan sesuai sebelum diproses. 
    
    3. Hubungkan dengan sistem lain seperti gateway pembayaran.

7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?

    Dengan menggunakan gRPC, pengembang dapat merancang sistem yang lebih modular dan efisien, yang memungkinkan komunikasi yang lebih lancar antara layanan-layanan yang berbeda bahkan jika mereka ditulis dalam bahasa pemrograman yang berbeda atau berjalan di platform yang berbeda. gRPC mengurangi hambatan interoperabilitas antara komponen-komponen yang berbeda dalam sistem terdistribusi, memfasilitasi integrasi dengan teknologi dan platform lainnya secara lebih efektif.    

8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?

    Advantage:
    
    * Multiplexing memungkinkan banyak permintaan HTTP untuk diproses secara bersamaan melalui satu koneksi TCP, mengurangi latensi dan mempercepat waktu muat halaman.

    * Kompresi header mengurangi overhead yang disebabkan oleh ukuran besar header pada HTTP/1.1, meningkatkan efisiensi penggunaan bandwidth.

    * Server push memungkinkan server untuk mengirimkan sumber daya tambahan kepada klien tanpa diminta, meningkatkan kecepatan pengiriman konten kepada klien.

    Disadvantage:

    * Kompleksitas implementasi yang lebih tinggi dan keterbatasan dukungan di beberapa server dan klien

9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?

    Request-response model dari REST APIs memungkinkan klien untuk membuat permintaan ke server dan menerima respons dari server sebagai tanggapan atas permintaan tersebut. Model mengikuti pola satu arah di mana klien mengirim permintaan dan menunggu respons dari server sebelum melakukan tindakan selanjutnya. gRPC menawarkan kemampuan bidirectional streaming yang memungkinkan komunikasi real-time antara klien dan server. Dengan gRPC, klien dan server dapat saling mengirim pesan secara asinkron dalam bentuk aliran yang kontinu. Hal ini memungkinkan respons dari server dapat dikirim kepada klien secara real-time tanpa menunggu permintaan baru dari klien.

10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?

    gRPC menggunakan Protocol Buffers mewajibkan definisi skema data sebelumnya, menghasilkan struktur data yang terstruktur dan konsisten di seluruh sistem. Sementara, dalam REST API menggunakan JSON, struktur data lebih fleksibel. Namun, gRPC memastikan konsistensi dan validitas data secara keseluruhan, sementara JSON dapat meningkatkan kompleksitas dan risiko kesalahan dalam pengelolaan data.