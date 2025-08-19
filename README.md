# Kütüphane Otomasyon Rest Api (Spring Boot)

Bu proje, Spring Boot framework'ü kullanarak modern bir kütüphane otomasyon sistemi geliştirmeyi amaçlamaktadır. Proje, RESTful API'ler aracılığıyla kitap yönetimi işlemlerini gerçekleştirir ve JSON formatında veri alışverişi yapar.

## Teknolojiler

- **Java 17+**
- **Spring Boot 3.x**
- **Spring Web (REST API)**
- **Spring Data JPA**
- **H2 Database (In-Memory)**
- **Maven**
- **Spring Boot DevTools**

## Proje Yapısı

```
src/main/java/com/kutuphane/
├── KutuphaneSistemiApplication.java
├── controller/
│   └── KitapController.java
├── entity/
│   └── Kitap.java
├── repository/
│   └── KitapRepository.java
├── service/
│   ├── KitapService.java
│   └── impl/
│       └── KitapServiceImpl.java
└── dto/
    ├── KitapRequestDto.java
    └── KitapResponseDto.java
```

## Özellikler

### REST API Endpoints

- **POST /api/kitaplar** - Yeni kitap ekleme
- **GET /api/kitaplar** - Tüm kitapları listeleme
- **GET /api/kitaplar/yazar/{yazarAdi}** - Belirli yazara ait kitapları listeleme
- **GET /api/kitaplar/sayisi** - Toplam kitap sayısını getirme
- **GET /api/kitaplar/{id}** - ID'ye göre kitap getirme
- **PUT /api/kitaplar/{id}** - Kitap güncelleme
- **DELETE /api/kitaplar/{id}** - Kitap silme

## Kullanılan Spring Boot Konuları

- **Spring Boot Starter Web** (REST API geliştirme)
- **Spring Data JPA** (Veritabanı işlemleri)
- **Entity ve Repository katmanları**
- **Service katmanı ve Dependency Injection**
- **DTO (Data Transfer Object) kullanımı**
- **Exception Handling (@ControllerAdvice)**
- **Validation (@Valid, @NotNull, @NotBlank)**
- **H2 Console entegrasyonu**

## Kurulum ve Çalıştırma

### Gereksinimler
- Java 17 veya üzeri
- Maven 3.6+

### Adımlar
1. Projeyi klonlayın veya indirin
2. Terminal/Command Prompt'ta proje klasörüne gidin
3. Aşağıdaki komutu çalıştırın:
```bash
mvn spring-boot:run
```
4. Uygulama http://localhost:8080 adresinde çalışmaya başlayacaktır
5. H2 veritabanı konsolu: http://localhost:8080/h2-console

## API Kullanım Örnekleri

### 1. Kitap Ekleme (POST)
**URL:** `POST http://localhost:8080/api/kitaplar`

**Request Body (JSON):**
```json
{
  "kitapAdi": "Sefiller",
  "yazar": "Victor Hugo",
  "sayfaSayisi": 1200
}
```

**Response:**
```json
{
  "id": 1,
  "kitapAdi": "Sefiller",
  "yazar": "Victor Hugo",
  "sayfaSayisi": 1200,
  "eklenmetarihi": "2024-01-15T10:30:00"
}
```

### 2. Tüm Kitapları Listeleme (GET)
**URL:** `GET http://localhost:8080/api/kitaplar`

**Response:**
```json
[
  {
    "id": 1,
    "kitapAdi": "Sefiller",
    "yazar": "Victor Hugo",
    "sayfaSayisi": 1200,
    "eklenmetarihi": "2024-01-15T10:30:00"
  },
  {
    "id": 2,
    "kitapAdi": "Suç ve Ceza",
    "yazar": "Fyodor Dostoyevski",
    "sayfaSayisi": 650,
    "eklenmetarihi": "2024-01-15T10:35:00"
  }
]
```

### 3. Yazara Göre Kitapları Listeleme (GET)
**URL:** `GET http://localhost:8080/api/kitaplar/yazar/Victor Hugo`

**Response:**
```json
[
  {
    "id": 1,
    "kitapAdi": "Sefiller",
    "yazar": "Victor Hugo",
    "sayfaSayisi": 1200,
    "eklenmetarihi": "2024-01-15T10:30:00"
  },
  {
    "id": 3,
    "kitapAdi": "Notre Dame'ın Kamburu",
    "yazar": "Victor Hugo",
    "sayfaSayisi": 400,
    "eklenmetarihi": "2024-01-15T10:40:00"
  }
]
```

### 4. Toplam Kitap Sayısı (GET)
**URL:** `GET http://localhost:8080/api/kitaplar/sayisi`

**Response:**
```json
{
  "toplamSayi": 3
}
```

## Postman/İnsomnia Test Koleksiyonu

Proje ile birlikte `api-test-collection.json` dosyası sağlanmıştır. Bu dosyayı Postman veya İnsomnia'ya import ederek tüm API endpoint'lerini test edebilirsiniz.

## Veritabanı

Proje H2 in-memory veritabanı kullanır. Uygulama her başlatıldığında veriler sıfırlanır.

### H2 Console Erişimi
- **URL:** http://localhost:8080/h2-console
- **JDBC URL:** jdbc:h2:mem:kutuphanedatabase
- **Username:** sa
- **Password:** (boş)

## Geliştirme Önerileri

1. **Entity Validasyonları:** `@NotBlank`, `@Min`, `@Max` gibi validasyon annotasyonları kullanın
2. **Exception Handling:** Custom exception sınıfları oluşturun
3. **Unit Testler:** `@SpringBootTest` ve `@WebMvcTest` kullanarak testler yazın
4. **Swagger Dokumentasyonu:** SpringDoc OpenAPI 3 ekleyin
5. **Logging:** SLF4J ile loglama ekleyin
6. **Kalıcı Veritabanı:** MySQL veya PostgreSQL entegrasyonu yapın

## Bonus Özellikler (İleri Seviye)

- **Pagination:** Sayfalama desteği ekleyin
- **Sorting:** Sıralama parametreleri ekleyin
- **Search:** Kitap adında arama yapma
- **File Upload:** Kitap kapağı resmi yükleme
- **JWT Authentication:** Güvenlik katmanı ekleme

## Proje Değerlendirme Kriterleri

1. **Kod Organizasyonu:** Katmanlı mimari doğru uygulanmış mı?
2. **REST API Tasarımı:** HTTP methodları ve status kodları doğru mu?
3. **Exception Handling:** Hata durumları uygun şekilde yönetilmiş mi?
4. **Validation:** Input validasyonları yapılmış mı?
5. **Documentation:** API endpoint'leri düzgün dokümante edilmiş mi?
