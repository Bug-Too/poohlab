---
title: Privacy Policy
---

# Monos Privacy Policy

**Effective date: 15 September 2026**

| | |
| --- | --- |
| App | Monos for iPhone (iOS 17 or later; iPhone only) |
| Bundle identifier | `com.poohlab.monos` |
| Developer | Purich Seenuallae, Thailand (Apple Developer Team `PXSW8GXFUZ`) |
| Purchases | No in-app purchases, no subscription. The app contains no purchase flow. |
| Language | English interface. Amounts are shown in Thai baht (THB). |
| Contact | purichseenuallae@gmail.com |

## The short version

Monos has no account, no server, and no networking code of any kind. Your cards, your expenses, and any receipt photos you attach are written to a private container on your own iPhone and never leave it. There is no analytics, no crash reporting, no advertising, no tracking, and no third-party SDK. Nobody, including the developer, can see what you record in Monos. The only way anything leaves the device is when you yourself tap Backup or Export and choose where to send the file. Deleting the app deletes the data.

## 1. What Monos does

Monos is a personal expense and credit-card tracker. You add your cards by hand, you record what you spend, and the app shows you what you have spent this month, how much credit you have left, and where your money went. Optionally it can photograph a receipt and attach it to an expense, and it can remind you before a statement closes or a payment falls due.

Monos is **not** connected to any bank. It does not link to accounts, import transactions, read statements, initiate payments, or check balances anywhere. It has no Open Banking integration and no card-scanning feature. Everything it knows is what you typed into it. It is a private record you keep for yourself, not a financial service, and it gives no financial, tax, or investment advice.

## 2. What is stored on your device, and why

Monos stores the following on your iPhone. None of it is transmitted anywhere.

| What is stored | Why it is needed |
| --- | --- |
| For each card: the name you gave it, the **last four digits only**, the credit limit, the statement day and due day, a colour, and an optional annual renewal date | To show the card, work out remaining credit for the current statement cycle, and schedule the reminders you asked for |
| Optionally, a link marking one card as sharing another card's credit limit, and the order you arranged your cards in | So a shared limit is counted once across the cards that share it, and so your cards stay in the order you chose |
| Optionally, a manually entered opening balance and the date you entered it | So you can correct the running total to match your real statement |
| For each expense: the title you typed, the amount, the category you picked, whether you paid by cash or card, which card, the date, and an optional note | These are the records the app exists to keep, and the totals and charts are calculated from them |
| Optionally, a receipt photograph attached to an expense | Because you took it and attached it |
| Five settings: whether onboarding is finished, whether balances are hidden, whether due-date reminders are on, whether renewal reminders are on, and the appearance preference | So the app opens in the state you left it in |

### Where and how it is stored

- Cards and expenses are stored in a SwiftData (SQLite) database inside the shared App Group container `group.com.poohlab.monos` on the device.
- That container is shared only between Monos and its own home screen widget, so the widget can show today's spending without a server. It is not shared with any other app, service, or device.
- Receipt photographs are held as external files referenced by the database, in the same private container. Before being saved, a photo is scaled down and re-encoded as a JPEG so it stays small.
- The "hide balances" setting is stored in the same App Group so the widget honours it too. The other four settings are stored in the app's own `UserDefaults`. Together these are the only reason Monos declares the UserDefaults API category in its privacy manifest, with Apple's reason codes `CA92.1` (app-specific settings) and `1C8F.1` (settings shared with the app's own extension).
- This data sits in the app's private container with the system's default file protection, which means it is covered by your iPhone's normal encrypted backup if you back the device up to iCloud or a computer. That backup is between you and Apple; Monos plays no part in it and has no access to it.
- When a save fails, Monos writes a single diagnostic line to the iPhone's own system log recording that a save failed. It never logs card numbers, expense titles, notes, or amounts, and the system log stays on your device.

## 3. What Monos does not collect

Monos does not collect, and has no way to collect:

- **No account.** No sign-up, no sign-in, no email address, name, phone number, username, or password. Monos never asks who you are.
- **No full card numbers.** There is no field for a full card number, expiry date, CVV, cardholder name, PIN, or bank login. The app stores at most the last four digits, which you type yourself as a label so you can tell your cards apart.
- **No bank connection.** No Open Banking, no aggregator, no screen scraping, no SMS or email parsing, no statement import, and no payment initiation.
- **No analytics, no crash reporting, no telemetry, no usage measurement** of the app itself.
- **No advertising**, no ad identifier (IDFA), no advertising network, no marketing profile.
- **No tracking**, in the App Store sense or any other sense. Your data is never linked to data from other companies or apps.
- **No third-party SDKs.** Monos uses only Apple's own frameworks: SwiftUI, SwiftData, WidgetKit, Charts, AVFoundation, UserNotifications, UniformTypeIdentifiers, UIKit and Foundation.
- **No network code at all.** The app contains no HTTP client, no socket code, no cloud SDK, and no iCloud or CloudKit sync. There is no server to send anything to, and no AI or machine-learning service is contacted. This is not a policy promise layered over a network feature; the capability does not exist in the app.
- **No location, contacts, calendar, photo library, microphone, health, or Bluetooth access.** Monos declares no permission-usage descriptions for these because it never asks for them.
- **No payment data.** There are no in-app purchases and no purchase flow, so no billing information passes through the app.

Monos's App Store privacy manifest (`PrivacyInfo.xcprivacy`) declares tracking as `false`, an **empty** list of collected data types, and a single accessed-API category: `UserDefaults`, with reasons `CA92.1` and `1C8F.1`.

## 4. Camera and notifications

These are the only two permissions Monos ever asks for, and the app works without either.

**Camera.** Monos asks for camera access only at the moment you tap to photograph a receipt. The photo is written straight into the app's private container and attached to that expense. It is never uploaded, and it is not added to your photo library. Monos does not request photo library access at all, so it cannot read the pictures you already have. If you decline, every other part of the app continues to work; you simply record expenses without receipts. You can withdraw the permission at any time in the iPhone's Settings.

**Notifications.** If you allow them, Monos schedules **local** reminders through iOS: a few days before a payment is due, on the day a statement closes, and thirty days before an annual fee if you entered a renewal date. These are scheduled on the device by iOS itself. There is no push server, no device token, and nothing is sent anywhere to trigger them. A reminder names the card label you chose, such as "KBank Visa •••• 4242", and is shown only on your own device. Turning the reminders off in Settings cancels them.

## 5. Backup, export and restore

This is the only route by which anything you recorded can leave your iPhone, and it runs only when you start it.

- **Backup Data** writes a JSON file containing your cards and expenses, including receipt photographs, to a temporary location and hands it to the standard iOS share sheet.
- **Export All (CSV)** writes a spreadsheet of your expenses in the same way.
- In both cases **you choose the destination** in Apple's own share sheet: Files, AirDrop, Mail, a messaging app, or anything else installed. Monos does not choose for you, does not upload in the background, and has no default destination. Once you hand the file to another app or service, that file is governed by the privacy policy of wherever you sent it, not by this one.
- **Restore from Backup** reads a JSON file you pick yourself through the iOS file picker. Monos reads only the file you selected. Restoring adds records the app does not already have and leaves existing ones untouched.

Treat an exported file as you would a bank statement: it contains your full spending history in plain form.

## 6. The home screen widget

The widget shows today's, this week's and this month's totals, a short trend, and which card falls due next. It reads the same on-device database directly and contacts nothing. It honours the "hide balances" setting, and it asks iOS to redact amounts on the Lock Screen while the device is locked. If you would rather show nothing at all, remove the widget or turn on Hide balances.

## 7. Children's use

Monos is a personal finance tool for the person who owns the iPhone and is not designed for or directed at children. It does not knowingly collect information from anyone, of any age, because it does not collect information at all. There is no sign-up, so no age is ever requested or recorded.

## 8. Retention and deletion

Because nothing is collected, there is nothing held anywhere for the developer to retain, disclose, or delete on your behalf. Your records stay on your iPhone for as long as you keep them.

- **Delete one expense or card** by opening it and choosing Delete.
- **Delete everything** in Settings, under Data, with "Delete All Data". This permanently removes every card and expense from the device, including attached receipt photographs.
- **Delete the app** and iOS removes its container, which takes the database, the receipts and the settings with it. Any pending reminders are removed with it.
- Files you exported yourself are outside the app; delete those wherever you sent them.

A copy may still exist in a device backup you made earlier. That backup belongs to you and is removed according to Apple's terms, not by Monos.

## 9. No international transfer of data

Monos transmits nothing, so there is no transfer of personal data to any country, and no processor, sub-processor, or third-party recipient anywhere in the world. There is nothing to disclose under a data-transfer heading because no transfer occurs.

Because no personal data is collected or processed by the developer, the rights that apply to a data controller under Thailand's Personal Data Protection Act, the EU and UK GDPR, and similar laws have no data to operate on here. You already hold the only copy, and you can read, correct, export or destroy it directly in the app at any time.

## 10. Security

Your records are protected by the security of the iPhone itself: the app's private container, which other apps cannot read, and the device's own encryption while it is locked. Keeping a passcode or Face ID enabled, and keeping iOS up to date, is what protects this data in practice.

Monos does not add a separate app lock in this release, so anyone who can unlock your iPhone and open the app can see your records. If that matters to you, the Hide balances setting replaces amounts with asterisks on screen.

There is no server to breach, no credentials to steal, and no transmission to intercept.

## 11. Changes to this policy

If a future version of Monos collects or transmits anything, this policy will be updated before that version is released, and the effective date at the top will change. Material changes will be described in the App Store release notes for the version that introduces them. This page is the current policy for the version on the App Store.

## 12. Contact

Questions about this policy, or about privacy in Monos, can be sent to **purichseenuallae@gmail.com**.

---

# นโยบายความเป็นส่วนตัวของ Monos

**วันที่มีผลบังคับใช้: 15 กันยายน 2026**

| | |
| --- | --- |
| แอป | Monos สำหรับ iPhone (iOS 17 ขึ้นไป เฉพาะ iPhone) |
| Bundle identifier | `com.poohlab.monos` |
| ผู้พัฒนา | ปุริช สีนวลแล ประเทศไทย (Apple Developer Team `PXSW8GXFUZ`) |
| การซื้อ | ไม่มีการซื้อในแอป ไม่มีค่าสมาชิกรายเดือน และในแอปไม่มีขั้นตอนการชำระเงิน |
| ภาษา | หน้าจอเป็นภาษาอังกฤษ จำนวนเงินแสดงเป็นเงินบาท (THB) |
| ติดต่อ | purichseenuallae@gmail.com |

## สรุปสั้น ๆ

Monos ไม่มีบัญชีผู้ใช้ ไม่มีเซิร์ฟเวอร์ และไม่มีโค้ดเชื่อมต่อเครือข่ายใด ๆ ทั้งสิ้น บัตร รายจ่าย และรูปใบเสร็จที่คุณแนบไว้ ถูกเขียนลงในพื้นที่ส่วนตัวบน iPhone ของคุณเองและไม่เคยออกไปไหน ไม่มีการเก็บสถิติการใช้งาน ไม่มีการรายงานข้อขัดข้อง ไม่มีโฆษณา ไม่มีการติดตาม และไม่มี SDK ของบุคคลที่สาม ไม่มีใครเห็นสิ่งที่คุณบันทึกใน Monos รวมถึงผู้พัฒนาเองด้วย ทางเดียวที่ข้อมูลจะออกจากเครื่องได้ คือเมื่อคุณกดสำรองข้อมูลหรือส่งออกด้วยตัวเอง แล้วเลือกปลายทางเอง การลบแอปคือการลบข้อมูล

## 1. Monos ทำอะไร

Monos เป็นแอปบันทึกรายจ่ายและติดตามบัตรเครดิตส่วนตัว คุณเพิ่มบัตรเอง บันทึกรายจ่ายเอง แล้วแอปจะแสดงว่าเดือนนี้ใช้ไปเท่าไร เหลือวงเงินเท่าไร และเงินหมดไปกับอะไร คุณจะถ่ายรูปใบเสร็จแนบไว้กับรายจ่ายก็ได้ และตั้งเตือนก่อนวันสรุปยอดหรือวันครบกำหนดชำระก็ได้

Monos **ไม่ได้** เชื่อมต่อกับธนาคารใด ๆ ไม่ผูกบัญชี ไม่ดึงรายการเดินบัญชี ไม่อ่านใบแจ้งยอด ไม่สั่งจ่ายเงิน และไม่ตรวจสอบยอดคงเหลือจากที่ไหนทั้งสิ้น ไม่มีการเชื่อมต่อ Open Banking และไม่มีฟีเจอร์สแกนบัตร ทุกอย่างที่แอปรู้คือสิ่งที่คุณพิมพ์เข้าไปเอง แอปนี้เป็นบันทึกส่วนตัวที่คุณเก็บไว้ดูเอง ไม่ใช่บริการทางการเงิน และไม่ได้ให้คำแนะนำด้านการเงิน ภาษี หรือการลงทุน

## 2. ข้อมูลอะไรถูกเก็บไว้บนเครื่องของคุณ และเก็บไปทำอะไร

Monos เก็บข้อมูลต่อไปนี้ไว้บน iPhone ของคุณ และไม่มีข้อมูลใดถูกส่งออกไปที่ใด

| สิ่งที่เก็บ | เก็บไปทำไม |
| --- | --- |
| ของแต่ละบัตร: ชื่อที่คุณตั้ง **เลขสี่ตัวท้ายเท่านั้น** วงเงิน วันสรุปยอด วันครบกำหนดชำระ สี และวันครบรอบค่าธรรมเนียมรายปี (ถ้ามี) | เพื่อแสดงบัตร คำนวณวงเงินคงเหลือของรอบบิลปัจจุบัน และตั้งเตือนตามที่คุณขอ |
| ถ้ามี: การทำเครื่องหมายว่าบัตรใบหนึ่งใช้วงเงินร่วมกับอีกใบ และลำดับบัตรที่คุณจัดไว้ | เพื่อให้วงเงินที่ใช้ร่วมกันถูกนับครั้งเดียว และให้บัตรเรียงตามที่คุณจัด |
| ถ้ามี: ยอดตั้งต้นที่คุณกรอกเอง พร้อมวันที่กรอก | เพื่อให้คุณปรับยอดสะสมให้ตรงกับใบแจ้งยอดจริงได้ |
| ของแต่ละรายจ่าย: ชื่อรายการที่คุณพิมพ์ จำนวนเงิน หมวดที่เลือก จ่ายเงินสดหรือบัตร บัตรใบไหน วันที่ และโน้ต (ถ้ามี) | นี่คือบันทึกที่เป็นเหตุผลของการมีแอปนี้ และยอดรวมกับกราฟทั้งหมดคำนวณจากข้อมูลนี้ |
| ถ้ามี: รูปใบเสร็จที่แนบกับรายจ่าย | เพราะคุณถ่ายและแนบไว้เอง |
| การตั้งค่า 5 อย่าง: ผ่านหน้าแนะนำแล้วหรือยัง ซ่อนยอดเงินหรือไม่ เปิดเตือนวันครบกำหนดหรือไม่ เปิดเตือนค่าธรรมเนียมรายปีหรือไม่ และโหมดสีที่เลือก | เพื่อให้แอปเปิดมาอยู่ในสถานะเดิมที่คุณทิ้งไว้ |

### เก็บไว้ที่ไหนและอย่างไร

- บัตรและรายจ่ายถูกเก็บในฐานข้อมูล SwiftData (SQLite) ภายใน App Group container ชื่อ `group.com.poohlab.monos` บนเครื่อง
- container นี้ถูกใช้ร่วมกันเฉพาะระหว่าง Monos กับวิดเจ็ตหน้าจอโฮมของตัวเองเท่านั้น เพื่อให้วิดเจ็ตแสดงยอดใช้จ่ายวันนี้ได้โดยไม่ต้องมีเซิร์ฟเวอร์ ไม่ได้ใช้ร่วมกับแอป บริการ หรืออุปกรณ์อื่นใด
- รูปใบเสร็จถูกเก็บเป็นไฟล์แยกที่ฐานข้อมูลอ้างถึง อยู่ใน container ส่วนตัวเดียวกัน ก่อนบันทึก รูปจะถูกย่อขนาดและบีบอัดเป็น JPEG เพื่อให้ไฟล์เล็ก
- การตั้งค่า "ซ่อนยอดเงิน" ถูกเก็บใน App Group เดียวกันเพื่อให้วิดเจ็ตทำตามด้วย ส่วนการตั้งค่าอีกสี่อย่างเก็บใน `UserDefaults` ของแอปเอง ทั้งหมดนี้คือเหตุผลเดียวที่ Monos ประกาศหมวด UserDefaults ไว้ในไฟล์ประกาศความเป็นส่วนตัว ด้วยรหัสเหตุผลของ Apple คือ `CA92.1` (การตั้งค่าเฉพาะแอป) และ `1C8F.1` (การตั้งค่าที่ใช้ร่วมกับส่วนขยายของแอปเอง)
- ข้อมูลนี้อยู่ใน container ส่วนตัวของแอปโดยใช้การป้องกันไฟล์ระดับปริยายของระบบ ซึ่งหมายความว่ามันถูกรวมอยู่ในข้อมูลสำรองที่เข้ารหัสตามปกติของ iPhone หากคุณสำรองข้อมูลขึ้น iCloud หรือลงคอมพิวเตอร์ การสำรองข้อมูลนั้นเป็นเรื่องระหว่างคุณกับ Apple โดย Monos ไม่มีส่วนเกี่ยวข้องและเข้าถึงไม่ได้
- เมื่อการบันทึกล้มเหลว Monos จะเขียนบรรทัดวินิจฉัยหนึ่งบรรทัดลงใน system log ของ iPhone เองว่าการบันทึกล้มเหลว โดยไม่เคยบันทึกเลขบัตร ชื่อรายการ โน้ต หรือจำนวนเงิน และ system log นั้นอยู่บนเครื่องของคุณ

## 3. ข้อมูลที่ Monos ไม่เก็บ

Monos ไม่เก็บ และไม่มีช่องทางจะเก็บได้ ดังนี้

- **ไม่มีบัญชีผู้ใช้** ไม่มีการสมัคร ไม่มีการเข้าสู่ระบบ ไม่มีอีเมล ชื่อ เบอร์โทร ชื่อผู้ใช้ หรือรหัสผ่าน Monos ไม่เคยถามว่าคุณเป็นใคร
- **ไม่มีเลขบัตรเต็ม** ไม่มีช่องกรอกเลขบัตรเต็ม วันหมดอายุ CVV ชื่อผู้ถือบัตร รหัส PIN หรือรหัสเข้าธนาคาร แอปเก็บได้มากที่สุดคือเลขสี่ตัวท้าย ซึ่งคุณพิมพ์เองเพื่อใช้เป็นป้ายกำกับให้แยกบัตรออกจากกัน
- **ไม่เชื่อมต่อธนาคาร** ไม่มี Open Banking ไม่มีตัวรวมบัญชี ไม่มีการดูดข้อมูลหน้าจอ ไม่อ่าน SMS หรืออีเมล ไม่นำเข้าใบแจ้งยอด และไม่สั่งจ่ายเงิน
- **ไม่มีการเก็บสถิติการใช้งาน ไม่มีการรายงานข้อขัดข้อง ไม่มี telemetry** และไม่มีการวัดการใช้งานตัวแอปเอง
- **ไม่มีโฆษณา** ไม่มีตัวระบุเพื่อการโฆษณา (IDFA) ไม่มีเครือข่ายโฆษณา และไม่มีการสร้างโปรไฟล์เพื่อการตลาด
- **ไม่มีการติดตาม (tracking)** ทั้งในความหมายของ App Store และความหมายอื่น ข้อมูลของคุณไม่เคยถูกเชื่อมโยงกับข้อมูลจากบริษัทหรือแอปอื่น
- **ไม่มี SDK ของบุคคลที่สาม** Monos ใช้เฉพาะเฟรมเวิร์กของ Apple เอง ได้แก่ SwiftUI, SwiftData, WidgetKit, Charts, AVFoundation, UserNotifications, UniformTypeIdentifiers, UIKit และ Foundation
- **ไม่มีโค้ดเชื่อมต่อเครือข่ายเลย** ในแอปไม่มีตัวเรียก HTTP ไม่มีโค้ดซ็อกเก็ต ไม่มี SDK คลาวด์ และไม่มีการซิงก์ iCloud หรือ CloudKit ไม่มีเซิร์ฟเวอร์ให้ส่งข้อมูลไป และไม่มีการติดต่อบริการ AI หรือ machine learning ใด ๆ นี่ไม่ใช่คำสัญญาที่วางทับฟีเจอร์เครือข่ายที่มีอยู่ แต่ความสามารถนั้นไม่มีอยู่ในแอปตั้งแต่ต้น
- **ไม่เข้าถึงตำแหน่งที่อยู่ รายชื่อผู้ติดต่อ ปฏิทิน คลังรูปภาพ ไมโครโฟน ข้อมูลสุขภาพ หรือ Bluetooth** Monos ไม่ได้ประกาศคำอธิบายการขอสิทธิเหล่านี้ไว้เลย เพราะไม่เคยขอ
- **ไม่มีข้อมูลการชำระเงิน** ไม่มีการซื้อในแอปและไม่มีขั้นตอนการชำระเงิน จึงไม่มีข้อมูลการเรียกเก็บเงินผ่านแอป

ไฟล์ประกาศความเป็นส่วนตัวของแอป (`PrivacyInfo.xcprivacy`) ระบุว่าไม่มีการติดตาม (`false`) ระบุรายการประเภทข้อมูลที่เก็บเป็น **รายการว่าง** และระบุหมวดการเข้าถึง API เพียงหมวดเดียว คือ `UserDefaults` ด้วยเหตุผล `CA92.1` และ `1C8F.1`

## 4. กล้องและการแจ้งเตือน

นี่คือสิทธิสองอย่างเดียวที่ Monos เคยขอ และแอปใช้งานได้โดยไม่ต้องให้ทั้งสองอย่าง

**กล้อง** Monos ขอสิทธิกล้องเฉพาะตอนที่คุณกดถ่ายรูปใบเสร็จเท่านั้น รูปถูกเขียนลง container ส่วนตัวของแอปโดยตรงและแนบกับรายจ่ายนั้น ไม่เคยถูกอัปโหลด และไม่ถูกเพิ่มเข้าคลังรูปภาพของคุณ Monos ไม่ได้ขอสิทธิเข้าคลังรูปภาพเลย จึงอ่านรูปที่คุณมีอยู่แล้วไม่ได้ ถ้าคุณปฏิเสธ ส่วนอื่นของแอปยังทำงานได้ทั้งหมด เพียงแต่บันทึกรายจ่ายโดยไม่มีใบเสร็จ คุณถอนสิทธินี้เมื่อใดก็ได้ในการตั้งค่าของ iPhone

**การแจ้งเตือน** หากคุณอนุญาต Monos จะตั้งการเตือน **แบบในเครื่อง** ผ่าน iOS ได้แก่ ก่อนถึงวันครบกำหนดชำระไม่กี่วัน ในวันที่สรุปยอด และล่วงหน้า 30 วันก่อนค่าธรรมเนียมรายปีหากคุณกรอกวันครบรอบไว้ การเตือนเหล่านี้ถูกตั้งบนเครื่องโดย iOS เอง ไม่มีเซิร์ฟเวอร์ push ไม่มี device token และไม่มีการส่งข้อมูลออกไปเพื่อสั่งให้เตือน ข้อความเตือนจะมีชื่อบัตรตามที่คุณตั้ง เช่น "KBank Visa •••• 4242" และแสดงเฉพาะบนเครื่องของคุณเอง การปิดการเตือนในหน้าตั้งค่าจะยกเลิกการเตือนทั้งหมด

## 5. การสำรองข้อมูล การส่งออก และการกู้คืน

นี่คือทางเดียวที่สิ่งที่คุณบันทึกไว้จะออกจาก iPhone ได้ และทำงานเมื่อคุณเป็นผู้เริ่มเท่านั้น

- **Backup Data** เขียนไฟล์ JSON ที่มีบัตรและรายจ่ายของคุณ รวมถึงรูปใบเสร็จ ลงในที่เก็บชั่วคราว แล้วส่งต่อให้แผงแชร์มาตรฐานของ iOS
- **Export All (CSV)** เขียนไฟล์ตารางรายจ่ายด้วยวิธีเดียวกัน
- ทั้งสองกรณี **คุณเป็นผู้เลือกปลายทาง** ในแผงแชร์ของ Apple เอง ไม่ว่าจะเป็น Files, AirDrop, อีเมล, แอปแชต หรืออะไรก็ตามที่ติดตั้งไว้ Monos ไม่เลือกให้ ไม่อัปโหลดเบื้องหลัง และไม่มีปลายทางตั้งต้น เมื่อคุณส่งไฟล์ให้แอปหรือบริการอื่นแล้ว ไฟล์นั้นอยู่ภายใต้นโยบายความเป็นส่วนตัวของปลายทางนั้น ไม่ใช่ของฉบับนี้
- **Restore from Backup** อ่านไฟล์ JSON ที่คุณเลือกเองผ่านตัวเลือกไฟล์ของ iOS โดย Monos อ่านเฉพาะไฟล์ที่คุณเลือกเท่านั้น การกู้คืนจะเพิ่มเฉพาะรายการที่แอปยังไม่มี และไม่แตะต้องรายการที่มีอยู่แล้ว

โปรดปฏิบัติต่อไฟล์ที่ส่งออกเหมือนใบแจ้งยอดจากธนาคาร เพราะในไฟล์มีประวัติการใช้จ่ายทั้งหมดของคุณในรูปแบบที่อ่านได้

## 6. วิดเจ็ตหน้าจอโฮม

วิดเจ็ตแสดงยอดของวันนี้ สัปดาห์นี้ และเดือนนี้ พร้อมแนวโน้มสั้น ๆ และบัตรที่จะถึงกำหนดชำระถัดไป โดยอ่านจากฐานข้อมูลบนเครื่องเดียวกันโดยตรงและไม่ติดต่อที่ใดเลย วิดเจ็ตทำตามการตั้งค่า "ซ่อนยอดเงิน" ด้วย และขอให้ iOS ปิดบังจำนวนเงินบนหน้าจอล็อกขณะที่เครื่องล็อกอยู่ หากคุณต้องการไม่ให้แสดงอะไรเลย ให้นำวิดเจ็ตออกหรือเปิด "ซ่อนยอดเงิน"

## 7. การใช้งานโดยเด็ก

Monos เป็นเครื่องมือจัดการการเงินส่วนบุคคลสำหรับเจ้าของ iPhone และไม่ได้ออกแบบมาเพื่อเด็กหรือมุ่งไปที่เด็ก แอปไม่เก็บข้อมูลจากผู้ใด ไม่ว่าอายุเท่าใด เพราะไม่ได้เก็บข้อมูลเลยตั้งแต่ต้น ไม่มีการสมัครใช้งาน จึงไม่มีการถามหรือบันทึกอายุ

## 8. การเก็บรักษาและการลบข้อมูล

เนื่องจากไม่มีการเก็บข้อมูลใด ๆ จึงไม่มีข้อมูลที่ใดให้ผู้พัฒนาต้องเก็บรักษา เปิดเผย หรือลบแทนคุณ บันทึกของคุณอยู่บน iPhone ตราบเท่าที่คุณเก็บไว้

- **ลบรายจ่ายหรือบัตรทีละรายการ** โดยเปิดรายการนั้นแล้วเลือกลบ
- **ลบทั้งหมด** ในหน้าตั้งค่า หัวข้อ Data ด้วยปุ่ม "Delete All Data" ซึ่งลบบัตรและรายจ่ายทุกรายการออกจากเครื่องอย่างถาวร รวมถึงรูปใบเสร็จที่แนบไว้
- **ลบแอป** แล้ว iOS จะลบ container ของแอปทิ้ง ซึ่งพาฐานข้อมูล รูปใบเสร็จ และการตั้งค่าไปด้วย การเตือนที่ตั้งค้างไว้จะถูกลบไปพร้อมกัน
- ไฟล์ที่คุณส่งออกเองอยู่นอกแอป กรุณาลบที่ปลายทางที่คุณส่งไป

ข้อมูลอาจยังคงอยู่ในไฟล์สำรองของเครื่องที่คุณทำไว้ก่อนหน้า ไฟล์สำรองนั้นเป็นของคุณ และถูกลบตามเงื่อนไขของ Apple ไม่ใช่โดย Monos

## 9. ไม่มีการโอนข้อมูลข้ามประเทศ

Monos ไม่ส่งข้อมูลใดออกไปเลย จึงไม่มีการโอนข้อมูลส่วนบุคคลไปยังประเทศใด และไม่มีผู้ประมวลผล ผู้ประมวลผลช่วง หรือผู้รับข้อมูลที่เป็นบุคคลที่สามในที่ใดในโลก ไม่มีสิ่งใดต้องเปิดเผยภายใต้หัวข้อการโอนข้อมูล เพราะไม่มีการโอนเกิดขึ้น

เนื่องจากผู้พัฒนาไม่ได้เก็บหรือประมวลผลข้อมูลส่วนบุคคลใด ๆ สิทธิที่ใช้กับผู้ควบคุมข้อมูลตามพระราชบัญญัติคุ้มครองข้อมูลส่วนบุคคลของไทย GDPR ของสหภาพยุโรปและสหราชอาณาจักร และกฎหมายทำนองเดียวกัน จึงไม่มีข้อมูลให้ใช้สิทธินั้นที่นี่ คุณถือสำเนาเดียวที่มีอยู่แล้ว และอ่าน แก้ไข ส่งออก หรือทำลายมันได้โดยตรงในแอปทุกเมื่อ

## 10. ความปลอดภัย

บันทึกของคุณได้รับการปกป้องด้วยความปลอดภัยของ iPhone เอง ได้แก่ container ส่วนตัวของแอปที่แอปอื่นอ่านไม่ได้ และการเข้ารหัสของเครื่องขณะล็อกอยู่ การตั้งรหัสผ่านหรือเปิด Face ID ไว้ และการอัปเดต iOS ให้เป็นปัจจุบัน คือสิ่งที่ปกป้องข้อมูลนี้ในทางปฏิบัติ

Monos เวอร์ชันนี้ยังไม่มีการล็อกแอปแยกต่างหาก ดังนั้นผู้ที่ปลดล็อก iPhone ของคุณและเปิดแอปได้ จะเห็นบันทึกของคุณ หากเรื่องนี้สำคัญกับคุณ การตั้งค่า "ซ่อนยอดเงิน" จะแทนที่จำนวนเงินบนหน้าจอด้วยเครื่องหมายดอกจัน

ไม่มีเซิร์ฟเวอร์ให้ถูกเจาะ ไม่มีข้อมูลรับรองให้ถูกขโมย และไม่มีการส่งข้อมูลให้ถูกดักฟัง

## 11. การเปลี่ยนแปลงนโยบายนี้

หาก Monos เวอร์ชันในอนาคตมีการเก็บหรือส่งข้อมูลใด ๆ นโยบายฉบับนี้จะถูกปรับปรุงก่อนที่เวอร์ชันนั้นจะออก และวันที่มีผลบังคับใช้ด้านบนจะเปลี่ยนไป การเปลี่ยนแปลงที่มีสาระสำคัญจะถูกอธิบายไว้ในบันทึกการอัปเดตบน App Store ของเวอร์ชันที่นำการเปลี่ยนแปลงนั้นมา หน้านี้คือนโยบายปัจจุบันสำหรับเวอร์ชันที่อยู่บน App Store

## 12. ติดต่อ

คำถามเกี่ยวกับนโยบายฉบับนี้ หรือเกี่ยวกับความเป็นส่วนตัวใน Monos ส่งมาได้ที่ **purichseenuallae@gmail.com**
