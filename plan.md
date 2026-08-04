# Kişisel Website — Mimari Plan

## 1. Linkler / Projeler / Sosyal
- **Instagram:** @caganbaris36 (sitedeki iletişim butonu)
- **Telefon:** tıklanabilir `tel:` linki (chatbot'a soru sorulursa numara doğrudan paylaşılmıyor, kullanıcı butona yönlendiriliyor)
- **AI Asistan (chatbot):** Statik bir "hakkımda" metni yerine, ziyaretçinin bana dair soru sorabileceği bir sohbet asistanı ekledim. Asistan yalnızca `profile.md` içindeki bilgiye dayanıyor, uydurma yapmıyor ve jailbreak denemelerine karşı korumalı.

## 2. Görsel Planlama
- **Tema:** Koyu/siyah zemin üzerine pastel/neon aurora blob'lar (canvas ile, fare hareketine tepki veren parallax)
- **Tipografi:** Başlık için `Fraunces` (serif, karakterli), gövde metni için `Inter`
- **Kart tasarımı:** Glassmorphism — yarı saydam, blur'lu koyu paneller
- **Kontrast:** İsimdeki Türkçe karakterlerin (`ğ`) net görünmesi için font ağırlığı ve arkasına drop-shadow eklendi
- **Hareket:** Arka planda yavaşça süzülen parıldayan parçacıklar (aurora'nın üstünde ikinci bir katman)

## 3. Kişiye Özel Dokunuş
- **Character/interaktif öğe:** Sağ altta sabit bir chat butonu — açılınca 3 hazır soru chip'i ("Çağan kim?", "Hangi alanlarla ilgileniyor?", "Ona nasıl ulaşabilirim?") ile başlıyor, kullanıcı serbest soru da yazabiliyor
- **Kişiselleştirme:** Asistan 3. şahıs anlatımla konuşuyor, bilmediği bir şey sorulursa bunu açıkça söyleyip alternatif konu öneriyor
- **Mobil uyum:** Chat paneli mobilde `visualViewport` API'siyle klavye açıldığında boyutunu ayarlıyor, input kaybolmuyor

## 4. Teknik Mimari
```
Frontend (index.html, statik)
  → sağ alt chat widget
  → /api/chat (Vercel serverless function)
      → sistem promptu + profile.md içeriği birleştirilir
      → Bedrock (Gemma modeli) çağrılır
      → cevap frontend'e döner
```
- API anahtarı yalnızca backend'de (`BEDROCK_API_KEY` env variable), `.env` `.gitignore`'da
- Deploy: GitHub → Vercel (otomatik deploy, `main` branch push'unda tetiklenir)
