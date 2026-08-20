<div align="center">
  <img src="./assets/khon-kaen-dino-icon.png" width="150" alt="Khon Kaen Dino Explorer icon" />

  # Khon Kaen Dino Explorer

  **แอปแนะนำ 10 สถานที่สำคัญในจังหวัดขอนแก่น พร้อมแผนที่แบบเต็มหน้าจอ**

  `Expo` · `React Native` · `TypeScript` · `React Native Maps`
</div>

---

## เกี่ยวกับโปรเจกต์

Khon Kaen Dino Explorer เป็นแอป Point of Interest (POI) สำหรับสำรวจสถานที่สำคัญในจังหวัดขอนแก่น ผู้ใช้สามารถเลือกสถานที่จากรายการเพื่อดูตำแหน่ง หมุด และป้ายชื่อบนแผนที่ได้ทันที

ตัวแอปใช้ธีมไดโนเสาร์สีเหลือง ซึ่งเชื่อมโยงกับแหล่งค้นพบไดโนเสาร์และภาพจำของจังหวัดขอนแก่น ออกแบบด้วยโทนน้ำเงินเข้ม–ทองให้มีบรรยากาศคล้ายพิพิธภัณฑ์และแอปท่องเที่ยวสมัยใหม่

## ฟีเจอร์หลัก

- แสดงรายชื่อสถานที่สำคัญในขอนแก่นจำนวน 10 แห่ง
- เลือกสถานที่แล้วแผนที่จะเคลื่อนไปยังพิกัดของสถานที่นั้น
- แสดง Marker และป้ายกำกับชื่อสถานที่บนแผนที่
- แสดงประเภท ที่อยู่ คำอธิบาย และค่า Latitude/Longitude
- เปิดแผนที่แบบเต็มหน้าจอ เลื่อนและซูมได้
- มีปุ่ม `◎` สำหรับเลื่อนกลับมายังหมุดที่เลือก
- รองรับ Google Maps บน Android และ Apple Maps บน iOS
- ไม่ขอ Location permission เพราะใช้พิกัด POI ที่กำหนดไว้ล่วงหน้า

## สถานที่ทั้ง 10 แห่ง

| ลำดับ | สถานที่ | ประเภท |
|---:|---|---|
| 1 | มหาวิทยาลัยขอนแก่น | การศึกษา |
| 2 | บึงแก่นนคร | สวนสาธารณะ |
| 3 | พระมหาธาตุแก่นนคร | ศาสนาและวัฒนธรรม |
| 4 | ศาลหลักเมืองขอนแก่น | สถานที่สำคัญ |
| 5 | เซ็นทรัล ขอนแก่น | ศูนย์การค้า |
| 6 | สถานีรถไฟขอนแก่น | การเดินทาง |
| 7 | ตลาดต้นตาล | ตลาดและอาหาร |
| 8 | พิพิธภัณฑสถานแห่งชาติ ขอนแก่น | พิพิธภัณฑ์ |
| 9 | ศูนย์ประชุมและแสดงสินค้านานาชาติขอนแก่น | ศูนย์ประชุม |
| 10 | ท่าอากาศยานขอนแก่น | การเดินทาง |

## เทคโนโลยีที่ใช้

- Expo SDK 54
- React Native 0.81
- React 19
- TypeScript
- React Native Maps

## วิธีติดตั้งและเปิดแอป

ต้องติดตั้ง [Node.js](https://nodejs.org/) และ Expo Go บนมือถือก่อน

```bash
git clone https://github.com/Sojjyuu/khon-kaen-dino-explorer.git
cd khon-kaen-dino-explorer
npm install
npx expo start --clear
```

จากนั้นเปิด Expo Go แล้วสแกน QR Code โดยให้มือถือและคอมพิวเตอร์เชื่อมต่อเครือข่ายเดียวกัน

หากเชื่อมต่อผ่าน LAN ไม่ได้ สามารถใช้ Tunnel ได้:

```bash
npx expo start --tunnel
```

## คำสั่งตรวจสอบโปรเจกต์

```bash
npm run typecheck
npm run check
```

โปรเจกต์ผ่าน TypeScript check และทดสอบสร้าง JavaScript bundle สำหรับ Android/iOS แล้ว

## โครงสร้างโปรเจกต์

```text
khon-kaen-poi/
├── assets/                         โลโก้และไอคอนแอป
├── src/
│   ├── components/PoiMap.tsx       แผนที่ หมุด ป้ายชื่อ และ Full-screen map
│   ├── data/pointsOfInterest.ts    ข้อมูล POI ทั้ง 10 แห่ง
│   ├── screens/PoiExplorerScreen.tsx
│   ├── theme/colors.ts             ชุดสีของแอป
│   └── types/poi.ts                TypeScript type ของ POI
├── App.tsx
├── app.config.ts
└── package.json
```

## Android Production Build

Expo Go ใช้ทดสอบงานพื้นฐานได้ แต่ Android Production Build ต้องเปิด Maps SDK for Android และกำหนด Google Maps API key โดยจำกัดการใช้งานด้วย:

- Android package: `com.sojjyu.khonkaenpoi`
- SHA-1 ของ signing certificate ที่ใช้สร้างแอป

เก็บ API key ใน EAS Environment Variables ชื่อ `GOOGLE_MAPS_ANDROID_API_KEY` และสร้าง binary ใหม่ เพราะ key ถูกฝังอยู่ใน native application

```bash
npx eas-cli env:create --name GOOGLE_MAPS_ANDROID_API_KEY --environment production --visibility secret
npx eas-cli build --profile production --platform android
```

> ห้ามอัปโหลด `.env`, API key, `node_modules` หรือโฟลเดอร์ `.expo` ขึ้น GitHub

## ผู้จัดทำ

โปรเจกต์รายวิชาการพัฒนาแอปพลิเคชันด้วย Expo และ React Native
