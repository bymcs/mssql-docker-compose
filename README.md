# 🛢️ MS SQL Server Docker Kurulumu

Bu repository, Docker kullanarak Microsoft SQL Server'ı hızlı bir şekilde çalıştırmanızı sağlayan yapılandırmayı içerir.

## 📋 İçerik

- [Gereksinimler](#gereksinimler)
- [Kurulum](#kurulum)
- [SQL Server Sürümleri](#sql-server-sürümleri)
- [Bağlantı Bilgileri](#bağlantı-bilgileri)
- [Volume Yönetimi](#volume-yönetimi)
- [Çevre Değişkenleri](#çevre-değişkenleri)
- [Yararlı Docker Komutları](#yararlı-docker-komutları)
- [Sorun Giderme](#sorun-giderme)

## 🔧 Gereksinimler

- Docker Engine (20.10.0+)
- Docker Compose (2.0.0+)
- En az 2GB RAM

## 🚀 Kurulum

1. Repository'yi klonlayın veya `docker-compose.yml` dosyasını bilgisayarınıza indirin.
2. Terminal veya komut istemcisini açın ve dosyanın bulunduğu dizine gidin.
3. Aşağıdaki komutu çalıştırın:

```bash
docker compose up -d
```

## 🏷️ SQL Server Sürümleri

Bu proje SQL Server 2019 kullanmaktadır. Docker Hub'da bulunan önemli MS SQL etiketleri:

| Etiket | Açıklama |
|--------|----------|
| `2022-latest` | SQL Server 2022 (en yeni sürüm) |
| `2019-latest` | SQL Server 2019 (bu projede kullanılan) |
| `2017-latest` | SQL Server 2017 |
| `2019-CU18-ubuntu-20.04` | Belirli bir Cumulative Update ile 2019 |
| `2019-GDR-ubuntu-20.04` | Security update paketi içeren 2019 |

## 🔌 Bağlantı Bilgileri

SQL Server'a bağlanmak için:

- **Server**: `localhost,1433`
- **Authentication**: SQL Server Authentication
- **Username**: `sa`
- **Password**: `YourStrong@Passw0rd`

Bağlantı için kullanabileceğiniz araçlar:
- SQL Server Management Studio (SSMS)
- Azure Data Studio
- Visual Studio Code (mssql eklentisi ile)
- DBeaver veya başka bir SQL istemcisi

## 💾 Volume Yönetimi

Veritabanı dosyaları `mssql_data` adlı Docker volume'ünde saklanır. Volume bilgilerini görmek için:

```bash
docker volume inspect mssql_data
```

Volume içeriğine erişmek için:

```bash
docker exec -it mssql_server bash
cd /var/opt/mssql
ls -la
```

## 🔐 Çevre Değişkenleri

| Değişken | Açıklama | Değer |
|----------|----------|-------|
| `ACCEPT_EULA` | Lisans anlaşmasını kabul etmek için gerekli | `Y` |
| `SA_PASSWORD` | System Administrator şifresi | `YourStrong@Passw0rd` |

Ek çevre değişkenleri (isteğe bağlı):
- `MSSQL_PID`: Ürün sürümü (Developer, Express, Standard, Enterprise, vb.)
- `MSSQL_MEMORY_LIMIT_MB`: Maksimum bellek kullanımı
- `MSSQL_BACKUP_DIR`: Yedekleme dizini
- `MSSQL_DATA_DIR`: Veri dosyaları dizini
- `MSSQL_LOG_DIR`: Log dosyaları dizini

## 🐳 Yararlı Docker Komutları

```bash
# Container'ı başlatma
docker compose up -d

# Container'ı durdurma
docker compose down

# Container loglarını görüntüleme
docker logs mssql_server

# Container'a bağlanma
docker exec -it mssql_server bash

# SQL Server durumunu kontrol etme (container içinde)
/opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P YourStrong@Passw0rd -Q "SELECT @@VERSION"
```

## ⚠️ Sorun Giderme

- **Bağlantı Hataları**: Port çakışması olmadığından emin olun.
- **Container Başlamıyor**: Bellek gereksinimleri karşılandığından emin olun (min. 2GB).
- **Şifre Hatası**: SA şifresi en az 8 karakter olmalı ve büyük harf, küçük harf, sayı ve özel karakter içermelidir.
- **Yetki Sorunları**: Windows'ta Docker Desktop'ın dosya paylaşım izinlerini kontrol edin.

---

📚 **Referanslar**
- [Microsoft SQL Server on Docker Hub](https://hub.docker.com/_/microsoft-mssql-server)
- [SQL Server Configuration for Docker](https://learn.microsoft.com/en-us/sql/linux/sql-server-linux-configure-environment-variables)