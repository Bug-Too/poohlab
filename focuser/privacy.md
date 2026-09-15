---
title: Privacy Policy
---

# Focuser Privacy Policy

**Effective date: 15 September 2026**

| | |
| --- | --- |
| App | Focuser for iPhone (iOS 17 or later; iPhone only) |
| Bundle identifier | `com.poohlab.focuser` |
| Developer | Purich Seenuallae, Thailand (Apple Developer Team `PXSW8GXFUZ`) |
| Price | Free. No in-app purchases, no subscription, no renewals. |
| Languages | Thai on Thai-language iPhones, English on every other device language. |
| Contact | purichseenuallae@gmail.com |

## The short version

Focuser has no account, no server, and no networking code of any kind. Everything the app remembers — your task titles, your temporary-access reasons, and the record of days you finished your list — is written to a private container on your own iPhone and never leaves it. There is no analytics, no crash reporting, no advertising, no tracking, and no third-party SDK. Nobody, including the developer, can see what you write in Focuser. Deleting the app deletes the data.

## 1. What Focuser does, and what it is not

Each day, measured in Asia/Bangkok time, you write 1 to 3 focus tasks in your own words, confirm the list — which freezes it for that day — and then mark each task done. When every task on the confirmed list is marked done, the apps you chose yourself unlock until midnight Thailand time. Completion is **self-reported**: Focuser records that you tapped done; it does not check, measure, or verify that the task actually happened, and a mark can be taken back on the same day. There is also a temporary-access option — ten elapsed minutes, once per Thailand day, after you write a reason — which does not count as finishing your list.

Focuser is a voluntary self-control tool. It is not parental control, it is not a monitoring or reporting product, and it is not a security control: it does not prevent the owner of the iPhone from changing iOS settings, withdrawing Focuser's Screen Time permission, or deleting the app. It makes no claim about verified learning, grades, or total screen time, and it is not a medical or therapeutic product.

## 2. What is stored on your device, and why

Focuser stores the following on your iPhone. None of it is transmitted anywhere.

| What is stored | Why it is needed |
| --- | --- |
| The titles of today's 1–3 focus tasks, as you typed them | They are the list you confirm and mark done; they are shown back to you on the Today screen |
| The time you confirmed the list, and the time you marked each task done | To freeze the list for the day, to decide when the list is finished, and to let you take a mark back |
| A record for each day you finished your whole list: the task titles as they stood and the time of completion | To show the "Your progress" section, which displays the most recent seven days |
| The last day on which you earned the daily unlock | So the unlock survives an app restart and ends at Thailand midnight rather than being granted twice |
| The reason you wrote for temporary access, with its start and expiry time | The rule requires a written reason; the expiry time restores restrictions after ten elapsed minutes |
| The Thailand days on which the temporary allowance was used | So the once-per-day allowance cannot be taken twice |
| Your selection of apps, categories, and website domains to restrict, as received from Apple's picker | So restrictions can be applied to exactly what you chose. These are opaque Screen Time tokens (see section 4) |
| A single true/false flag recording that you finished onboarding | So setup is not shown again on every launch |

### Where and how it is stored

- Product state and your app selection are versioned JSON files (`state.json`, `selection.json`) in the shared App Group container `group.com.poohlab.focuser` on the device.
- That container is shared only between Focuser and its own on-device extensions (the Device Activity monitor and the two shield extensions), so a background callback can apply restrictions correctly. It is not shared with any other app, service, or device.
- The files are **excluded from backup**, so they are not copied into an iCloud or computer backup, and they are **protected until the first unlock after a restart** (`completeUntilFirstUserAuthentication`), so they cannot be read while the iPhone has not been unlocked since powering on. Writes are atomic and guarded by a file lock so the app and its extensions never read a half-written file.
- The onboarding flag is a single boolean in the app's own `UserDefaults`. This is the only reason Focuser's privacy manifest declares the UserDefaults API category, with Apple's reason code `CA92.1` (app-specific settings).
- Focuser's Device Activity monitor writes one diagnostic line to the iPhone's own system log when it reconciles restrictions, naming which callback ran and, on failure, the error text. It never logs task titles or reasons, and the system log stays on your device.
- Some rows in Focuser open Apple's own Settings app (for the per-app language switch, or to fix Screen Time permission). Focuser receives nothing back from Settings other than the permission state iOS reports to it.

## 3. What Focuser does not collect

Focuser does not collect, and has no way to collect:

- **No account.** No sign-up, no sign-in, no email address, name, phone number, username, or password. Focuser never asks who you are.
- **No analytics, no crash reporting, no telemetry, no usage measurement** of the app itself.
- **No advertising**, no ad identifier (IDFA), no advertising network, no marketing profile.
- **No tracking**, in the App Store sense or any other sense. Your data is never linked to data from other companies or apps.
- **No third-party SDKs.** Focuser uses only Apple's own frameworks (SwiftUI, Family Controls, Managed Settings, Device Activity, Foundation) and one small first-party Swift package written for this app.
- **No network code at all.** The app contains no HTTP client, no socket code, no cloud SDK, and no iCloud or CloudKit sync. There is no server to send anything to, and no AI or machine-learning service is contacted. This is not a policy promise layered over a network feature; the capability does not exist in the app.
- **No location, contacts, calendar, photos, camera, microphone, health, or Bluetooth access.** Focuser declares no permission-usage descriptions for these because it never asks for them.
- **No payment data.** The first release is free with no in-app purchases and no purchase flow, so no billing information passes through the app.
- **No verification of your tasks.** There is no timer requirement, no screenshot, no quiz, no photo, no document upload, and no content check. The app only records the tap you made.
- **No browsing or app-usage history.** See section 4.

Focuser's App Store privacy manifest (`PrivacyInfo.xcprivacy`) declares tracking as `false`, an **empty** list of collected data types, and a single accessed-API reason: `UserDefaults` with reason `CA92.1`.

## 4. Apple Screen Time permissions (Family Controls)

To restrict apps at all, Focuser needs your permission through Apple's Screen Time system:

- **You grant the authorization.** iOS asks you directly; Focuser cannot grant it to itself. You can withdraw it later in the iPhone's Settings, under Screen Time. If it is withdrawn, Focuser stops restricting anything and says so on screen rather than pretending it is still enforcing the rule.
- **You choose what is restricted, in Apple's own picker.** The list of apps, categories, and website domains is presented by iOS, not by Focuser, and it runs outside Focuser's process.
- **Focuser receives only opaque tokens.** What the picker hands back is a set of tokens that Apple deliberately makes meaningless outside the system: Focuser cannot turn a token back into an app's name, bundle identifier, or icon. The app therefore does not know which apps you chose — only how many items you selected — and it stores and re-applies those tokens without ever being able to read them.
- **Focuser never sees your usage or browsing history.** It does not read Screen Time reports, app-usage totals, time spent, notification counts, Safari history, or any record of what you opened. The Device Activity framework is used only as a clock: one repeating schedule for the Bangkok day (00:00:00–23:59:59), plus two short non-repeating schedules that bring the ten-minute temporary access to an end. Those callbacks read the record already stored on your device and adjust the restrictions; they report nothing.
- **Restrictions are applied to Focuser's own Managed Settings store only.** When your list is finished, Focuser clears only the shields it set itself. Other Screen Time limits, other apps' restrictions, and any parental or system restrictions on the device are untouched.
- **The shield screen** you see over a restricted app is drawn by Focuser's own extensions. They read the stored record on the device to name the work that is left and to handle the Close button. They write nothing and send nothing.

Family Controls is used here for one adult managing their own device. Focuser does not create a parent-child relationship, does not request a guardian's approval, and has nothing to send to anyone else.

## 5. Children's use

Focuser's pilot audience is university students in Thailand aged 20 or over, who manage their own study routine, although the app is useful to anyone. It is not designed for or directed at children, and it is **not a parental-control product**: there is no parent or teacher dashboard, no report to a guardian or a school, and no way for one person to watch another person's list.

Because Focuser collects no personal information from anyone and sends nothing off the device, it collects no personal information from children either — knowingly or otherwise. There is no profile to build, no record for the developer to hold, and nothing for a parent or guardian to request or have erased from us. If a younger person uses the app on their own iPhone, everything they write stays in that iPhone's local container and is removed by deleting the history in the app, or by deleting the app.

## 6. Retention and deletion

Nothing is retained by the developer, because nothing is ever received. On the device:

- **Your data stays until you remove it.** The app does not expire or prune your records on its own. The "Your progress" section shows the most recent seven days; records of earlier completed days remain in the local file until you delete history or delete the app.
- **The daily reset** at midnight Thailand time starts a new list. Finished tasks do not recur; tasks you did not finish are carried into a new, unconfirmed draft for the new day.
- **"Delete history"** (Settings → Your data) removes every past completed-day record and clears the stored temporary-access reason. It deliberately keeps today's list, today's earned unlock, and the fact that today's temporary allowance has been used, so clearing history cannot relock a day you already earned, grant a second temporary access, or reset an access period that is still running. The deletion is immediate, local, and cannot be undone.
- **Deleting the app** removes its App Group container and everything described in section 2 with it. Because those files are excluded from backup, they are not waiting in an iCloud or computer backup either. You may also want to remove Focuser's Screen Time authorization in the iPhone's Settings after deleting it.
- **There is nothing for the developer to delete, export, or return**, and no request can make the developer produce your task titles, reasons, or history: no copy of them has ever existed outside your iPhone.

Requests to access, correct, export, or erase what Focuser holds are therefore carried out by you, on your own device, using the actions above. If you believe the developer holds data about you, write to purichseenuallae@gmail.com and you will get an honest answer.

## 7. No international transfer of data

Focuser stores everything locally on your iPhone and contains no code that opens a network connection. As a result there is no transfer of your data to the developer, to a hosting provider, to a cloud service, or to any processor, sub-processor, or partner — inside Thailand or outside it. The rules in Thailand's Personal Data Protection Act, and in comparable laws elsewhere, about sending personal data across borders do not come into play here, because no personal data is sent anywhere at all.

## 8. Security

- Your data never travels, so it is not exposed in transit and there is no server that could be breached.
- On the device it is protected by the iPhone's own encryption, your passcode or biometric lock, and iOS's App Group sandbox, plus the file protection and backup exclusion described in section 2.
- Honestly stated limitation: this is device-level protection. Anyone who can unlock your iPhone can open Focuser and read your list, your history, and your temporary-access reason, exactly as they could read your notes. Focuser adds no separate password of its own.
- A physical-device build of Focuser intentionally fails to start rather than silently falling back to private storage if it cannot open its shared container, so your data and the enforcement it drives never drift apart.

## 9. Changes to this policy

If this policy changes, the updated text is published at this same address and the effective date at the top is changed. Because Focuser has no account and no contact details for you, this page — together with the App Store listing that links to it — is the notice: there is no mailing list to write to you on. Changes that materially affect what is stored or how the app behaves will be described plainly rather than folded silently into the text, and the App Store listing's own privacy details will be updated at the same time.

## 10. Contact

Questions about this policy, or about how Focuser handles data, can be sent to **purichseenuallae@gmail.com**. The developer is Purich Seenuallae, based in Thailand; replies are in Thai or English.

---

# นโยบายความเป็นส่วนตัวของ Focuser

**วันที่มีผลบังคับใช้: 15 กันยายน 2026**

| | |
| --- | --- |
| แอป | Focuser สำหรับ iPhone (iOS 17 ขึ้นไป เฉพาะ iPhone) |
| Bundle identifier | `com.poohlab.focuser` |
| ผู้พัฒนา | ปุริช สีนวลแล (Purich Seenuallae) ประเทศไทย (Apple Developer Team `PXSW8GXFUZ`) |
| ราคา | ฟรี ไม่มีการซื้อในแอป ไม่มีการสมัครสมาชิก ไม่มีการต่ออายุอัตโนมัติ |
| ภาษา | ภาษาไทยบน iPhone ที่ตั้งภาษาไทย และภาษาอังกฤษสำหรับภาษาอื่น |
| ติดต่อ | purichseenuallae@gmail.com |

## สรุปสั้น ๆ

Focuser ไม่มีบัญชีผู้ใช้ ไม่มีเซิร์ฟเวอร์ และไม่มีโค้ดเชื่อมต่อเครือข่ายใด ๆ ทุกอย่างที่แอปจำไว้ ทั้งชื่องานที่คุณเขียน เหตุผลของการเข้าใช้ชั่วคราว และบันทึกวันที่คุณทำรายการครบ ถูกเขียนเก็บไว้ในพื้นที่ส่วนตัวบน iPhone ของคุณเอง และไม่ถูกส่งออกไปที่ใดเลย ไม่มีการเก็บสถิติการใช้งาน ไม่มีการรายงานข้อขัดข้อง ไม่มีโฆษณา ไม่มีการติดตาม และไม่มี SDK ของบุคคลที่สาม ไม่มีใครมองเห็นสิ่งที่คุณเขียนใน Focuser รวมถึงผู้พัฒนาเองด้วย การลบแอปคือการลบข้อมูลทั้งหมด

## 1. Focuser ทำอะไร และไม่ใช่อะไร

ในแต่ละวันตามเวลาประเทศไทย (Asia/Bangkok) คุณเขียนงานโฟกัส 1–3 อย่างด้วยคำของคุณเอง กด "ยืนยันรายการวันนี้" ซึ่งทำให้รายการนั้นถูกล็อกไว้สำหรับวันนั้น แล้วค่อยกดว่าทำเสร็จแต่ละข้อ เมื่อทุกข้อในรายการที่ยืนยันแล้วถูกกดว่าทำเสร็จ แอปที่คุณเลือกไว้เองจะเปิดใช้ได้จนถึงเที่ยงคืนตามเวลาประเทศไทย

การทำเสร็จเป็น **การยืนยันด้วยตัวคุณเอง** Focuser บันทึกว่าคุณกดปุ่มเท่านั้น ไม่ได้ตรวจ ไม่ได้วัด และไม่ได้ยืนยันว่างานนั้นเกิดขึ้นจริง และคุณสามารถยกเลิกการกดนั้นได้ภายในวันเดียวกัน นอกจากนี้ยังมีการเข้าใช้ชั่วคราว คือ 10 นาทีตามเวลาที่เดินไป ใช้ได้วันละครั้งตามวันของประเทศไทย หลังจากคุณเขียนเหตุผล และไม่นับว่าเป็นการทำรายการของวันนั้นครบ

Focuser เป็นเครื่องมือควบคุมตัวเองด้วยความสมัครใจ ไม่ใช่ระบบควบคุมโดยผู้ปกครอง ไม่ใช่ระบบเฝ้าดูหรือรายงานพฤติกรรม และไม่ใช่มาตรการความปลอดภัย แอปไม่ได้ป้องกันเจ้าของ iPhone จากการแก้การตั้งค่า iOS การถอนสิทธิ Screen Time หรือการลบแอปออก แอปไม่ได้อ้างว่าตรวจสอบการเรียนรู้ได้ ไม่ได้รับประกันผลการเรียนหรือการลดเวลาหน้าจอโดยรวม และไม่ใช่ผลิตภัณฑ์ทางการแพทย์หรือการรักษา

## 2. ข้อมูลอะไรถูกเก็บไว้บนเครื่องของคุณ และเก็บไปทำอะไร

Focuser เก็บข้อมูลต่อไปนี้ไว้บน iPhone ของคุณ และไม่มีข้อมูลใดถูกส่งออกไปที่ใด

| สิ่งที่ถูกเก็บ | เหตุผลที่จำเป็น |
| --- | --- |
| ชื่องานโฟกัส 1–3 อย่างของวันนี้ ตามที่คุณพิมพ์ | เป็นรายการที่คุณยืนยันและกดว่าทำเสร็จ และถูกแสดงกลับให้คุณเห็นบนหน้าวันนี้ |
| เวลาที่คุณยืนยันรายการ และเวลาที่คุณกดว่าแต่ละงานเสร็จ | เพื่อล็อกรายการไว้สำหรับวันนั้น เพื่อรู้ว่ารายการครบเมื่อใด และเพื่อให้ย้อนการกดได้ |
| บันทึกของแต่ละวันที่คุณทำรายการครบ ได้แก่ ชื่องานตามที่เป็นในวันนั้นและเวลาที่ทำครบ | เพื่อแสดงส่วน "ความก้าวหน้าของคุณ" ซึ่งแสดง 7 วันล่าสุด |
| วันล่าสุดที่คุณได้รับการปลดล็อกประจำวัน | เพื่อให้การปลดล็อกคงอยู่แม้ปิดแอป และสิ้นสุดที่เที่ยงคืนเวลาไทย โดยไม่ถูกให้ซ้ำสองครั้ง |
| เหตุผลที่คุณเขียนเพื่อขอเข้าใช้ชั่วคราว พร้อมเวลาเริ่มและเวลาหมด | กติกากำหนดให้ต้องเขียนเหตุผล และเวลาหมดใช้เพื่อกลับมาจำกัดแอปหลังผ่านไป 10 นาที |
| วันของประเทศไทยที่ใช้สิทธิเข้าใช้ชั่วคราวไปแล้ว | เพื่อไม่ให้ใช้สิทธิวันละครั้งซ้ำได้ |
| รายการแอป หมวดหมู่ และโดเมนเว็บไซต์ที่คุณเลือกจำกัด ตามที่ได้รับจากตัวเลือกของ Apple | เพื่อจำกัดเฉพาะสิ่งที่คุณเลือกไว้ ข้อมูลนี้เป็นโทเคน Screen Time ที่อ่านความหมายไม่ได้ (ดูข้อ 4) |
| ค่าจริง/เท็จค่าเดียวที่บันทึกว่าคุณผ่านขั้นตอนเริ่มต้นใช้งานแล้ว | เพื่อไม่ต้องแสดงขั้นตอนตั้งค่าซ้ำทุกครั้งที่เปิดแอป |

### เก็บไว้ที่ไหนและอย่างไร

- สถานะของแอปและรายการที่คุณเลือกถูกเก็บเป็นไฟล์ JSON ที่ระบุเวอร์ชัน (`state.json`, `selection.json`) อยู่ใน App Group ที่ใช้ร่วมกันชื่อ `group.com.poohlab.focuser` บนเครื่อง
- พื้นที่นี้ใช้ร่วมกันเฉพาะระหว่าง Focuser กับส่วนขยายของตัวเองบนเครื่องเดียวกัน (ตัวเฝ้าดู Device Activity และส่วนขยายหน้าจอกั้นสองตัว) เพื่อให้การจำกัดแอปทำงานถูกต้องแม้แอปไม่ได้เปิดอยู่ ไม่ได้แบ่งให้แอปอื่น บริการอื่น หรืออุปกรณ์อื่นใด
- ไฟล์เหล่านี้ถูก **ยกเว้นจากการสำรองข้อมูล** จึงไม่ถูกคัดลอกเข้าไปในข้อมูลสำรองของ iCloud หรือของคอมพิวเตอร์ และถูก **ป้องกันไว้จนกว่าจะปลดล็อกเครื่องครั้งแรกหลังรีสตาร์ต** (`completeUntilFirstUserAuthentication`) จึงอ่านไม่ได้ในช่วงที่ยังไม่มีการปลดล็อก iPhone หลังเปิดเครื่อง การเขียนไฟล์เป็นแบบ atomic และมีการล็อกไฟล์ เพื่อให้แอปและส่วนขยายไม่อ่านไฟล์ที่เขียนค้างอยู่
- ค่าสถานะการเริ่มต้นใช้งานเป็นค่า boolean ค่าเดียวใน `UserDefaults` ของแอปเอง นี่เป็นเหตุผลเดียวที่ไฟล์ประกาศความเป็นส่วนตัวของ Focuser ระบุหมวด API ของ UserDefaults ด้วยรหัสเหตุผลของ Apple `CA92.1` (การตั้งค่าเฉพาะของแอป)
- ตัวเฝ้าดู Device Activity ของ Focuser เขียนบรรทัดบันทึกวินิจฉัยหนึ่งบรรทัดลงในระบบบันทึกของ iPhone เองเมื่อปรับการจำกัดแอป โดยระบุว่า callback ใดทำงาน และหากล้มเหลวจะระบุข้อความข้อผิดพลาด แอปไม่เคยบันทึกชื่องานหรือเหตุผลลงไป และบันทึกของระบบยังอยู่ในเครื่องของคุณ
- บางแถวในแอปเปิดแอปการตั้งค่าของ Apple เอง (สำหรับสลับภาษาเฉพาะแอป หรือแก้สิทธิ Screen Time) Focuser ไม่ได้รับสิ่งใดกลับมาจากการตั้งค่า นอกจากสถานะสิทธิที่ iOS แจ้งให้ทราบ

## 3. ข้อมูลที่ Focuser ไม่เก็บ

Focuser ไม่เก็บ และไม่มีช่องทางจะเก็บได้ ดังนี้

- **ไม่มีบัญชีผู้ใช้** ไม่มีการสมัคร ไม่มีการเข้าสู่ระบบ ไม่มีอีเมล ชื่อ เบอร์โทร ชื่อผู้ใช้ หรือรหัสผ่าน Focuser ไม่เคยถามว่าคุณเป็นใคร
- **ไม่มีการเก็บสถิติการใช้งาน ไม่มีการรายงานข้อขัดข้อง ไม่มี telemetry** และไม่มีการวัดการใช้งานตัวแอปเอง
- **ไม่มีโฆษณา** ไม่มีตัวระบุเพื่อการโฆษณา (IDFA) ไม่มีเครือข่ายโฆษณา และไม่มีการสร้างโปรไฟล์เพื่อการตลาด
- **ไม่มีการติดตาม (tracking)** ทั้งในความหมายของ App Store และความหมายอื่น ข้อมูลของคุณไม่เคยถูกเชื่อมโยงกับข้อมูลจากบริษัทหรือแอปอื่น
- **ไม่มี SDK ของบุคคลที่สาม** Focuser ใช้เฉพาะเฟรมเวิร์กของ Apple เอง (SwiftUI, Family Controls, Managed Settings, Device Activity, Foundation) และแพ็กเกจ Swift ขนาดเล็กที่เขียนขึ้นสำหรับแอปนี้เท่านั้น
- **ไม่มีโค้ดเชื่อมต่อเครือข่ายเลย** ในแอปไม่มีตัวเรียก HTTP ไม่มีโค้ดซ็อกเก็ต ไม่มี SDK คลาวด์ และไม่มีการซิงก์ iCloud หรือ CloudKit ไม่มีเซิร์ฟเวอร์ให้ส่งข้อมูลไป และไม่มีการติดต่อบริการ AI หรือ machine learning ใด ๆ นี่ไม่ใช่คำสัญญาที่วางทับฟีเจอร์เครือข่ายที่มีอยู่ แต่ความสามารถนั้นไม่มีอยู่ในแอปตั้งแต่ต้น
- **ไม่เข้าถึงตำแหน่งที่อยู่ รายชื่อผู้ติดต่อ ปฏิทิน รูปภาพ กล้อง ไมโครโฟน ข้อมูลสุขภาพ หรือ Bluetooth** Focuser ไม่ได้ประกาศคำอธิบายการขอสิทธิเหล่านี้ไว้เลย เพราะไม่เคยขอ
- **ไม่มีข้อมูลการชำระเงิน** เวอร์ชันแรกเป็นของฟรี ไม่มีการซื้อในแอปและไม่มีขั้นตอนการชำระเงิน จึงไม่มีข้อมูลการเรียกเก็บเงินผ่านแอป
- **ไม่มีการตรวจสอบงานของคุณ** ไม่มีข้อกำหนดเรื่องจับเวลา ไม่มีการถ่ายภาพหน้าจอ ไม่มีแบบทดสอบ ไม่มีการถ่ายรูป ไม่มีการอัปโหลดเอกสาร และไม่มีการตรวจเนื้อหา แอปบันทึกเพียงการกดของคุณ
- **ไม่มีประวัติการเข้าเว็บหรือประวัติการใช้แอป** ดูข้อ 4

ไฟล์ประกาศความเป็นส่วนตัวของแอป (`PrivacyInfo.xcprivacy`) ระบุว่าไม่มีการติดตาม (`false`) ระบุรายการประเภทข้อมูลที่เก็บเป็น **รายการว่าง** และระบุเหตุผลการเข้าถึง API เพียงรายการเดียว คือ `UserDefaults` ด้วยเหตุผล `CA92.1`

## 4. สิทธิ Screen Time ของ Apple (Family Controls)

การจำกัดแอปทำได้ก็เพราะคุณให้สิทธิผ่านระบบ Screen Time ของ Apple

- **คุณเป็นผู้ให้สิทธิ** iOS ถามคุณโดยตรง Focuser ให้สิทธิแก่ตัวเองไม่ได้ และคุณถอนสิทธิได้ภายหลังในการตั้งค่าของ iPhone หัวข้อ Screen Time หากสิทธิถูกถอน Focuser จะหยุดจำกัดแอปและแสดงตามความจริงบนหน้าจอ ไม่แสร้งว่ายังบังคับกติกาอยู่
- **คุณเลือกเองว่าจะจำกัดอะไร ในตัวเลือกของ Apple เอง** รายการแอป หมวดหมู่ และโดเมนเว็บไซต์ถูกแสดงโดย iOS ไม่ใช่โดย Focuser และทำงานอยู่นอกกระบวนการของ Focuser
- **Focuser ได้รับเพียงโทเคนที่อ่านความหมายไม่ได้** สิ่งที่ตัวเลือกส่งกลับมาเป็นชุดโทเคนที่ Apple ออกแบบให้ไม่มีความหมายนอกระบบ Focuser ไม่สามารถแปลงโทเคนกลับเป็นชื่อแอป bundle identifier หรือไอคอนได้ ดังนั้นแอปจึงไม่รู้ว่าคุณเลือกแอปใด รู้เพียงว่าคุณเลือกไว้กี่รายการ และเก็บกับนำโทเคนนั้นไปใช้ซ้ำโดยที่อ่านไม่ได้เลย
- **Focuser ไม่เคยเห็นประวัติการใช้งานหรือการเข้าเว็บของคุณ** แอปไม่อ่านรายงาน Screen Time ยอดเวลาการใช้แอป เวลาที่ใช้ไป จำนวนการแจ้งเตือน ประวัติ Safari หรือบันทึกใด ๆ ว่าคุณเปิดอะไร เฟรมเวิร์ก Device Activity ถูกใช้เป็นเพียงนาฬิกา คือตารางเวลาแบบทำซ้ำหนึ่งชุดสำหรับวันตามเวลากรุงเทพ (00:00:00–23:59:59) กับตารางเวลาแบบไม่ทำซ้ำสั้น ๆ อีกสองชุดที่ปิดการเข้าใช้ชั่วคราว 10 นาที callback เหล่านั้นอ่านข้อมูลที่เก็บอยู่ในเครื่องของคุณแล้วปรับการจำกัด ไม่ได้รายงานสิ่งใดออกไป
- **การจำกัดถูกใช้ผ่าน Managed Settings store ของ Focuser เท่านั้น** เมื่อรายการของคุณครบ Focuser ปลดเฉพาะการกั้นที่ตัวเองตั้งไว้ ขีดจำกัด Screen Time อื่น ๆ การจำกัดของแอปอื่น และการจำกัดของผู้ปกครองหรือของระบบบนเครื่อง ไม่ถูกแตะต้อง
- **หน้าจอกั้น** ที่คุณเห็นทับแอปที่ถูกจำกัด ถูกวาดโดยส่วนขยายของ Focuser เอง ส่วนขยายอ่านข้อมูลที่เก็บอยู่ในเครื่องเพื่อบอกว่ายังเหลืองานอะไร และเพื่อรองรับปุ่มปิด โดยไม่เขียนและไม่ส่งข้อมูลใด

Family Controls ถูกใช้ที่นี่ในกรณีผู้ใหญ่คนหนึ่งดูแลเครื่องของตัวเอง Focuser ไม่ได้สร้างความสัมพันธ์แบบผู้ปกครองกับบุตร ไม่ขอการอนุมัติจากผู้ปกครอง และไม่มีสิ่งใดจะส่งให้ผู้อื่น

## 5. การใช้งานโดยเด็ก

กลุ่มผู้ใช้นำร่องของ Focuser คือนักศึกษามหาวิทยาลัยในประเทศไทยที่อายุ 20 ปีขึ้นไป ซึ่งดูแลตารางการเรียนของตัวเอง แม้ว่าแอปจะเป็นประโยชน์กับใครก็ได้ แอปไม่ได้ออกแบบมาเพื่อเด็กและไม่ได้มุ่งไปที่เด็ก และ **ไม่ใช่ผลิตภัณฑ์ควบคุมโดยผู้ปกครอง** ไม่มีแดชบอร์ดสำหรับผู้ปกครองหรือครู ไม่มีการรายงานไปยังผู้ปกครองหรือสถานศึกษา และไม่มีช่องทางให้คนหนึ่งดูรายการของอีกคน

เนื่องจาก Focuser ไม่เก็บข้อมูลส่วนบุคคลจากใครเลยและไม่ส่งสิ่งใดออกจากเครื่อง จึงไม่มีการเก็บข้อมูลส่วนบุคคลจากเด็กด้วย ทั้งโดยรู้และไม่รู้ ไม่มีโปรไฟล์ให้สร้าง ไม่มีบันทึกที่ผู้พัฒนาถือไว้ และไม่มีสิ่งใดที่ผู้ปกครองต้องขอดูหรือขอให้ลบจากเรา หากผู้ใช้อายุน้อยใช้แอปบน iPhone ของตัวเอง ทุกสิ่งที่เขียนไว้จะอยู่ในพื้นที่เก็บข้อมูลบนเครื่องนั้น และถูกลบได้ด้วยการลบประวัติในแอป หรือการลบแอปออก

## 6. การเก็บรักษาและการลบข้อมูล

ผู้พัฒนาไม่ได้เก็บรักษาข้อมูลใดไว้ เพราะไม่เคยได้รับข้อมูลเลย บนเครื่องของคุณ

- **ข้อมูลของคุณอยู่จนกว่าคุณจะลบ** แอปไม่ได้ลบหรือตัดบันทึกของคุณเองโดยอัตโนมัติ ส่วน "ความก้าวหน้าของคุณ" แสดง 7 วันล่าสุด บันทึกของวันที่ทำครบก่อนหน้านั้นยังอยู่ในไฟล์บนเครื่องจนกว่าคุณจะลบประวัติหรือลบแอป
- **การเริ่มวันใหม่** ที่เที่ยงคืนเวลาประเทศไทยจะเริ่มรายการใหม่ งานที่ทำเสร็จแล้วไม่กลับมาซ้ำ งานที่ยังไม่เสร็จจะถูกยกไปเป็นฉบับร่างของวันใหม่ที่ยังไม่ได้ยืนยัน
- **"ลบประวัติ"** (การตั้งค่า → ข้อมูลของคุณ) ลบบันทึกของวันที่ทำครบทั้งหมดในอดีต และล้างเหตุผลการเข้าใช้ชั่วคราวที่เก็บไว้ โดยตั้งใจคงไว้ซึ่งรายการของวันนี้ การปลดล็อกที่ได้มาแล้วของวันนี้ และข้อเท็จจริงว่าสิทธิเข้าใช้ชั่วคราวของวันนี้ถูกใช้ไปแล้ว การล้างประวัติจึงไม่ทำให้วันที่ได้มาแล้วกลับไปถูกล็อก ไม่ให้สิทธิเข้าใช้ชั่วคราวเป็นครั้งที่สอง และไม่รีเซ็ตช่วงเวลาที่กำลังเดินอยู่ การลบเกิดขึ้นทันที อยู่บนเครื่อง และย้อนคืนไม่ได้
- **การลบแอป** จะลบพื้นที่ App Group ของแอปพร้อมทุกอย่างที่ระบุไว้ในข้อ 2 และเนื่องจากไฟล์เหล่านั้นถูกยกเว้นจากการสำรองข้อมูล จึงไม่มีค้างอยู่ในข้อมูลสำรองของ iCloud หรือของคอมพิวเตอร์ด้วย หลังลบแอปแล้วคุณอาจต้องการลบสิทธิ Screen Time ของ Focuser ในการตั้งค่าของ iPhone ด้วย
- **ไม่มีสิ่งใดให้ผู้พัฒนาลบ ส่งออก หรือส่งคืน** และไม่มีคำขอใดทำให้ผู้พัฒนาแสดงชื่องาน เหตุผล หรือประวัติของคุณได้ เพราะไม่เคยมีสำเนาของสิ่งเหล่านั้นอยู่นอก iPhone ของคุณ

ดังนั้นการขอเข้าถึง แก้ไข ส่งออก หรือลบข้อมูลที่ Focuser เก็บไว้ จึงเป็นสิ่งที่คุณทำได้เองบนเครื่องของคุณ ด้วยวิธีข้างต้น หากคุณเชื่อว่าผู้พัฒนาถือข้อมูลเกี่ยวกับคุณอยู่ โปรดเขียนมาที่ purichseenuallae@gmail.com แล้วคุณจะได้รับคำตอบตามความจริง

## 7. ไม่มีการส่งข้อมูลออกนอกประเทศ

Focuser เก็บทุกอย่างไว้บน iPhone ของคุณ และไม่มีโค้ดที่เปิดการเชื่อมต่อเครือข่าย จึงไม่มีการส่งข้อมูลของคุณไปยังผู้พัฒนา ผู้ให้บริการโฮสติ้ง บริการคลาวด์ หรือผู้ประมวลผล ผู้ประมวลผลช่วง หรือคู่ค้ารายใด ทั้งในประเทศไทยและนอกประเทศ ข้อกำหนดของพระราชบัญญัติคุ้มครองข้อมูลส่วนบุคคลของไทย และกฎหมายทำนองเดียวกันในที่อื่น เรื่องการส่งข้อมูลส่วนบุคคลข้ามแดน จึงไม่เข้ามาเกี่ยวข้องในกรณีนี้ เพราะไม่มีข้อมูลส่วนบุคคลถูกส่งไปที่ใดเลย

## 8. ความปลอดภัย

- ข้อมูลของคุณไม่เคยเดินทาง จึงไม่เสี่ยงถูกดักระหว่างทาง และไม่มีเซิร์ฟเวอร์ที่จะถูกเจาะได้
- บนเครื่อง ข้อมูลได้รับการปกป้องด้วยการเข้ารหัสของ iPhone เอง รหัสผ่านหรือการปลดล็อกด้วยชีวมิติของคุณ และแซนด์บ็อกซ์ App Group ของ iOS ร่วมกับการป้องกันไฟล์และการยกเว้นจากการสำรองข้อมูลตามที่ระบุในข้อ 2
- ข้อจำกัดที่ต้องบอกตามตรง นี่คือการป้องกันระดับเครื่อง ใครที่ปลดล็อก iPhone ของคุณได้ก็เปิด Focuser และอ่านรายการ ประวัติ และเหตุผลการเข้าใช้ชั่วคราวของคุณได้ เช่นเดียวกับที่อ่านโน้ตของคุณได้ Focuser ไม่ได้เพิ่มรหัสผ่านของตัวเองอีกชั้น
- บิลด์สำหรับเครื่องจริงของ Focuser ถูกทำให้หยุดทำงานตั้งแต่ต้นโดยเจตนา แทนที่จะเปลี่ยนไปใช้พื้นที่เก็บข้อมูลส่วนตัวอย่างเงียบ ๆ หากเปิดพื้นที่ที่ใช้ร่วมกันไม่ได้ เพื่อให้ข้อมูลของคุณกับการบังคับกติกาที่ใช้ข้อมูลนั้นไม่แยกออกจากกัน

## 9. การเปลี่ยนแปลงนโยบายนี้

หากนโยบายนี้เปลี่ยนแปลง ข้อความที่ปรับปรุงแล้วจะถูกเผยแพร่ที่ที่อยู่เดียวกันนี้ และวันที่มีผลบังคับใช้ด้านบนจะถูกแก้ตาม เนื่องจาก Focuser ไม่มีบัญชีผู้ใช้และไม่มีช่องทางติดต่อคุณ หน้านี้ พร้อมกับรายการใน App Store ที่ลิงก์มาที่นี่ จึงเป็นการแจ้งให้ทราบ ไม่มีรายชื่ออีเมลให้ส่งถึงคุณได้ การเปลี่ยนแปลงที่มีผลอย่างมีนัยสำคัญต่อสิ่งที่ถูกเก็บหรือต่อการทำงานของแอป จะถูกอธิบายอย่างตรงไปตรงมา ไม่ใช่สอดแทรกเข้าไปในเนื้อความอย่างเงียบ ๆ และรายละเอียดความเป็นส่วนตัวในรายการ App Store จะถูกปรับปรุงพร้อมกัน

## 10. ติดต่อ

คำถามเกี่ยวกับนโยบายนี้ หรือเกี่ยวกับวิธีที่ Focuser จัดการข้อมูล ส่งมาได้ที่ **purichseenuallae@gmail.com** ผู้พัฒนาคือปุริช สีนวลแล อยู่ในประเทศไทย ตอบกลับเป็นภาษาไทยหรือภาษาอังกฤษ