**Project Overview**

DATATHON 2026 — The Gridbreakers

Chào mừng: bạn đóng vai nhà khoa học dữ liệu cho một doanh nghiệp thương mại điện tử thời trang Việt Nam. Mục tiêu chính: dự báo doanh thu thuần (`Revenue`) theo ngày cho giai đoạn 01/01/2023 – 01/07/2024, trên nền dữ liệu huấn luyện 04/07/2012 – 31/12/2022.

**Dataset**
- **Scope**: 15 file CSV, chia thành 4 lớp: Master, Transaction, Analytical, Operational.
- **Key files**:
  - [products.csv](products.csv) — danh mục sản phẩm
  - [customers.csv](customers.csv) — thông tin khách hàng
  - [promotions.csv](promotions.csv) — chương trình khuyến mãi
  - [orders.csv](orders.csv), [order_items.csv](order_items.csv), [payments.csv](payments.csv) — giao dịch
  - [sales.csv](sales.csv) — doanh thu hàng ngày (train)
  - [sales_test.csv](sales_test.csv) — dữ liệu test (định dạng giống sample_submission)
  - [sample_submission.csv](sample_submission.csv) — mẫu nộp bài
  - [inventory.csv](inventory.csv), [web_traffic.csv](web_traffic.csv)

**Objective**
- Dự báo cột `Revenue` (doanh thu thuần hàng ngày) cho khoảng 01/01/2023 – 01/07/2024.
- Tập test không công bố; nộp file `submission.csv` giữ nguyên thứ tự dòng như `sample_submission.csv`.

**Evaluation Metrics**
- Bảng điểm trên Kaggle dùng đồng thời ba chỉ số: MAE, RMSE, R².

- Mean Absolute Error (MAE):
  $$\mathrm{MAE}=\frac{1}{n}\sum_{i=1}^n|F_i-A_i|$$

- Root Mean Squared Error (RMSE):
  $$\mathrm{RMSE}=\sqrt{\frac{1}{n}\sum_{i=1}^n(F_i-A_i)^2}$$

- Coefficient of Determination (R²):
  $$R^2=1-\frac{\sum_{i=1}^n(F_i-A_i)^2}{\sum_{i=1}^n(A_i-\bar{A})^2}$$

Trong đó $F_i$ là giá trị dự báo, $A_i$ là giá trị thực, và $\bar{A}$ là trung bình giá trị thực.

**Repository Notebooks & Files**
- [eda_ver0_1.ipynb](eda_ver0_1.ipynb) — khám phá dữ liệu, visualizations, insights.
- [eda_ver0_1_minh.ipynb](eda_ver0_1_minh.ipynb) — phiên bản EDA cá nhân/nhánh.
- [Feature_Engineering_and_Modeling.ipynb](Feature_Engineering_and_Modeling.ipynb) — pipeline feature engineering, CV, modeling thử nghiệm.
- [MCQ.ipynb](MCQ.ipynb) — file cho phần Trắc nghiệm (MCQ) hoặc notebook chứa đáp án/giải thích.

**Recommended Workflow**
1. Khám phá: mở [eda_ver0_1.ipynb](eda_ver0_1.ipynb) để hiểu seasonal, trend, outliers, missing data.
2. Kết hợp dữ liệu: join `sales.csv` với `web_traffic.csv`, `promotions.csv`, `inventory.csv`, và thông tin sản phẩm/khách hàng khi cần.
3. Tạo features thời gian (lag, rolling, calendar), event/promotions flags, traffic features, inventory signals.
4. Cross-validation: dùng time-series aware CV (rolling / expanding windows).
5. Mô hình: baseline (SARIMAX / ETS / Prophet), tree-based (LightGBM / CatBoost), ensemble và NN nếu cần.
6. Giải trình: SHAP / feature importance, và kiểm tra residuals theo thời gian.

**Submission**
- Tạo `submission.csv` cuối cùng theo đúng cấu trúc của [sample_submission.csv](sample_submission.csv) và giữ nguyên thứ tự.

**Setup & Run (suggested)**
1. Tạo môi trường Python (Windows example):

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

2. Nếu không có `requirements.txt`, cài tối thiểu:

```powershell
pip install pandas numpy matplotlib seaborn scikit-learn lightgbm shap jupyterlab
```

3. Chạy notebook bằng JupyterLab / Jupyter Notebook, hoặc convert script nếu cần.

**Tips & Good Practices**
- Xử lý ngày thiếu và outliers trước khi tạo lag features.
- Giữ một baseline đơn giản (naive / last-year / rolling mean) để so sánh.
- Tối ưu hoá theo MAE/RMSE; kiểm tra lỗi theo tuần/tháng để bắt pattern hệ thống.

**Citation**
- Datathon 2026. DATATHON 2026 - Vòng Sơ loại. https://kaggle.com/competitions/datathon-2026-round-1, 2026. Kaggle.

**Contact**
- Nếu cần mở rộng README (environment, requirements, scripts, CI), tôi có thể thêm hướng dẫn chạy, `requirements.txt`, và scripts tự động hoá.
