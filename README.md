# Siam Piwat Footfall Analytics Project 2026

โปรเจกต์วิเคราะห์และจัดทำรายงาน Footfall Analytics ร่วมกับ Siam Piwat เพื่อศึกษาพฤติกรรม สถิติ และรูปแบบการเข้าใช้บริการของผู้เยี่ยมชมห้างสรรพสินค้าครอบคลุมทั้งหมด 19 แห่ง (เช่น ห้างในเครือสยามพิวัฒน์, The Mall Group, และ Central Group)

---

## 📌 Scope & Objectives

โครงการนี้สรุปและวิเคราะห์ผลลัพธ์ออกมาเป็น 5 รายงานหลัก (Reports) โดยเน้นวิเคราะห์มิติข้อมูลสำคัญ ดังนี้:

* **Customer Types (ประเภทผู้เข้าใช้บริการ):**
  * `local_bmr`: ผู้ที่มีบ้านและสถานที่ทำงานอยู่ในเขตกรุงเทพฯ และปริมณฑล
  * `local_non_bmr`: ผู้ที่มีบ้านและสถานที่ทำงานอยู่นอกเขตกรุงเทพฯ และปริมณฑล
  * `foreigner`: ผู้ใช้บริการชาวต่างชาติ (ใช้ Tourist SIM หรือเปิด Data Roaming)
* **Demographics (ข้อมูลประชากรศาสตร์):** อายุ (`age`), เพศ (`gender`), และระดับความมั่งคั่ง (`affluence`)
* **Interests (ความสนใจทางดิจิทัล):** พฤติกรรมการใช้อินเทอร์เน็ต จำแนกตามประเภท Retail รวม 13 หมวดหมู่ (Categories)
* **Frequency Behavior (ความถี่การเยี่ยมชม):** ความถี่ในการเดินทางไปห้างสรรพสินค้าแต่ละแห่ง และระหว่างห้างสรรพสินค้า
* **Location Behavior (พฤติกรรมการเคลื่อนที่):** การกระจายตัวและการเดินทางไปยังสถานที่อื่น ๆ (Hop analysis)

---

## 🔄 Data Pipeline Workflow
* master_cellsite.ipynb
  * กำหนด Shape file ของห้างสรรพสินค้าเพื่อคัดเลือกเสาสัญญาณ (cell_site) ที่ครอบคลุมพื้นที่ห้างจริง
* Data_Preprocessing.ipynb
  * กวาดข้อมูล Footfall จาก Table trueanalytics_data.trueanalytics_bus.fact_cdr_geo_agg_hour_v2
  * จำแนก Customer Type และบันทึกเป็น Parquet บน DBFS ที่ path: dbfs:/Volumes/int-cu-siampiwat/staging/raw/proj_3/{par_month}_footfall.parquet
* prep_data_360.ipynb
  * Stamp ข้อมูล Demographics (age, gender, affluence) และ Digital Interest 13 Categories
* prep_data_flag_freq.ipynb
  * Stamp ความถี่การเข้าใช้บริการ ทั้งรายห้างและระหว่างห้างสรรพสินค้า

## 📁 Repository Structure

```text
tech-delivery-siampiwat-2026/
├── master_cellsite.ipynb        # กรองเสาสัญญาณ (Cell Site) ด้วย Shape file ของห้าง
├── Data_Preprocessing.ipynb     # กวาดข้อมูล Footfall, จำแนกประเภทลูกค้า และเซฟลง DBFS
├── prep_data_360.ipynb          # Stamp ข้อมูล Customer Profile 360 (Demo & Interest 13 Cats)
├── prep_data_flag_freq.ipynb    # Stamp ค่าความถี่ (Frequency) การเข้าใช้บริการรายห้าง/ระหว่างห้าง
├── full_report/                 # สคริปต์/สมุดโน้ตสำหรับสร้าง Full Reports
└── some_report/                 # สคริปต์/สมุดโน้ตสำหรับสร้าง Partial/Specific Reports

---
