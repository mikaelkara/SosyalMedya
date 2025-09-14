## [AGENTS.md](http://AGENTS.md) Dosyası

Bu dosya, Google Slayt ve Vids ile Sosyal Medya Video Oluşturma projesi için yapay zeka ajanlarına yönelik bilgi ve yönergeler içerir.

### Proje Genel Bakış

Bu proje, Google Slayt ve Vids araçlarını kullanarak sosyal medya için 60 saniyelik motivasyon videoları üretmeyi amaçlamaktadır. Türkçe ve İngilizce altyazılar ekleyerek evrensel bir yaklaşım benimsenmektedir. Proje, mevcut videoların işlenmesi ve otomatikleştirilmiş içerik üretimi üzerine odaklanmaktadır.

### Teknik Altyapı

- **Kullanılan Araçlar:** Google Colab, Google Drive, Google Slayt, Google Vids
- **Programlama Dili:** Python 3.9+
- **Temel Kütüphaneler:** OpenCV, MoviePy, PyDub, Google Text-to-Speech API, ffmpeg
- **Yapay Zeka Araçları:** GPT API, Google AI Studio API

### Kurulum Talimatları

```bash
# Google Colab ortamında gerekli kütüphanelerin kurulumu
!pip install opencv-python
!pip install moviepy
!pip install pydub
!pip install google-cloud-texttospeech
!pip install ffmpeg-python

# Google Drive bağlantısı
from google.colab import drive
drive.mount('/content/drive')

```

### Çalışma Akışı

1. **Video Analizi:** Sisteme yüklenen videoların süresini ve içeriğini analiz edin.
2. **Altyazı Üretimi:** Video içeriğine uygun altyazı metinleri oluşturun (Türkçe ve İngilizce).
3. **Ses Üretimi:** Text-to-speech teknolojisi ile altyazılar için sesli anlatım oluşturun.
4. **Video Birleştirme:** Orijinal video, ses ve altyazıyı birleştirin.
5. **Dağıtım:** Oluşturulan videoları sosyal medya platformlarına yükleyin.

### Kod Stil Kılavuzu

- **Dosya Yapısı:** Her modül ayrı bir .py dosyasında olmalıdır (video_processor.py, subtitle_generator.py, text_to_speech.py, vb.)
- **Dokümantasyon:** Tüm fonksiyonlar için docstrings kullanın (Google stil dokümantasyonu tercih edilir)
- **Değişken Adlandırma:** snake_case kullanın
- **Sınıf Adlandırma:** PascalCase kullanın
- **Sabitler:** BÜYÜK_HARFLERLE_VE_ALT_ÇİZGİ ile tanımlayın

### Test Talimatları

```python
# Video işleme modülünü test etme örneği
from video_processor import VideoProcessor

# Test videosu yolu
test_video_path = "/content/drive/MyDrive/test_videos/sample.mp4"

# Videonun süresini ve özelliklerini çıkarma
processor = VideoProcessor(test_video_path)
duration = processor.get_duration()
dimensions = processor.get_dimensions()

print(f"Video süresi: {duration} saniye")
print(f"Video boyutları: {dimensions[0]}x{dimensions[1]}")

```

### Otomatik İş Akışı

```python
# Tam otomatik iş akışı örneği
from video_processor import VideoProcessor
from subtitle_generator import SubtitleGenerator
from text_to_speech import TextToSpeech
from video_editor import VideoEditor

def process_video(video_path, output_path, language="tr"):
    # Video işleme
    processor = VideoProcessor(video_path)
    duration = processor.get_duration()
    
    # Altyazı üretimi
    subtitle_gen = SubtitleGenerator()
    subtitles = subtitle_gen.generate_for_duration(duration, language=language)
    
    # Ses üretimi
    tts = TextToSpeech()
    audio_path = tts.generate_audio(subtitles, language=language)
    
    # Video düzenleme
    editor = VideoEditor()
    final_video = editor.combine(
        video_path=video_path,
        audio_path=audio_path,
        subtitles=subtitles,
        output_path=output_path
    )
    
    return final_video

```

### Güvenlik Hususları

- **API Anahtarları:** Tüm API anahtarlarını ayrı bir .env dosyasında saklayın, koda doğrudan eklemekten kaçının
- **Telif Hakkı:** Kullanılan tüm içeriklerin telif hakkı durumunu kontrol edin
- **Veri Güvenliği:** Kullanıcı verilerini yerel olarak işleyin, mümkünse buluta yüklemekten kaçının

### Sorun Giderme

- **CUDA Hataları:** Google Colab'da CUDA hatası alırsanız, çalışma zamanı tipini GPU olarak değiştirin
- **RAM Yetersizliği:** Büyük videolarda RAM yetersizliği yaşarsanız, videoları daha küçük parçalara bölün
- **Drive Bağlantı Sorunları:** Drive bağlantısı düşerse, drive.mount('/content/drive', force_remount=True) kullanın

### Commit Mesajları

Commit mesajları şu formatı takip etmelidir:

```
[MOD]: Video işleme modülü eklendi
[FIX]: Altyazı zamanlaması sorunu çözüldü
[ENH]: TTS ses kalitesi iyileştirildi
[DOC]: Proje dokümantasyonu güncellendi

```

### İleri Seviye Özellikler (Gelecek)

- Tam otomatik içerik üretimi için GPT API entegrasyonu
- Video tarzına göre müzik seçimi yapan bir AI modülü
- İzleyici etkileşimlerini analiz eden performans dashboard'u
- Çoklu dil desteği (10+ dil)
