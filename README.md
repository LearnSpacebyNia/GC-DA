![image](https://github.com/user-attachments/assets/356d32f7-b064-492f-ba7a-89b45d5c71f5)
### Contoh Query Data
``` sql
INSERT INTO company (company_name, employee)
VALUES 
(
  'Tech Innovators',
  ARRAY[
    STRUCT(
      'Alice Johnson' AS name,
      ARRAY[
        STRUCT('New York' AS city, 'NY' AS state, '10001' AS zip),
        STRUCT('Los Angeles' AS city, 'CA' AS state, '90001' AS zip)
      ] AS emp_address,
      '29' AS age,
      STRUCT('alice.johnson@techinnovators.com' AS email, '123-456-7890' AS phone) AS emp_contact
    ),
    STRUCT(
      'Bob Smith' AS name,
      ARRAY[
        STRUCT('San Francisco' AS city, 'CA' AS state, '94105' AS zip),
        STRUCT('Miami' AS city, 'FL' AS state, '33101' AS zip)
      ] AS emp_address,
      '35' AS age,
      STRUCT('bob.smith@techinnovators.com' AS email, '098-765-4321' AS phone) AS emp_contact
    )
  ]
);
```
## Penjelasan :
1. Kolom company_name: Menyimpan nama perusahaan, seperti 'Tech Innovators'.
2. Kolom employee: Menyimpan array yang berisi STRUCT untuk setiap karyawan. Dalam contoh ini, ada dua karyawan (Alice Johnson dan Bob Smith), masing-masing dengan informasi emp_address yang berupa array (untuk alamat), age, dan emp_contact yang berupa STRUCT dengan email dan phone.

## Cara Membaca Tabel:
1. Setiap perusahaan (company_name) memiliki satu baris dalam tabel.
2. Kolom employee berisi array dari struktur data yang kompleks, di mana masing-masing elemen array mewakili seorang karyawan.
3. Setiap elemen karyawan (STRUCT) berisi nama, array dari alamat (emp_address), usia (age), dan kontak (emp_contact).

## Contoh Nyata
- company_name: Nama perusahaan, dalam contoh ini adalah 'Tech Innovators'.
- employee: Kolom yang menyimpan array STRUCT untuk setiap karyawan.
    1. Karyawan Pertama (Alice Johnson):
       - name: 'Alice Johnson'
       - emp_address: Array yang terdiri dari dua alamat:
       - Alamat pertama: 'New York, NY, 10001'
       - Alamat kedua: 'Los Angeles, CA, 90001'
       - age: '29'
       - emp_contact: STRUCT yang berisi:
       - email: 'alice.johnson@techinnovators.com'
       - phone: '123-456-7890'
  2. Karyawan Kedua (Bob Smith):
       - name: 'Bob Smith'
       - emp_address: Array yang terdiri dari dua alamat:
       - Alamat pertama: 'San Francisco, CA, 94105'
       - Alamat kedua: 'Miami, FL, 33101'
       - age: '35'
       - emp_contact: STRUCT yang berisi:
       - email: 'bob.smith@techinnovators.com'
       - phone: '098-765-4321'

### Contoh Akses Data

1. **Untuk mengakses nama karyawan pertama:**
   ```sql
   SELECT employee[OFFSET(0)].name FROM company WHERE company_name = 'Tech Innovators';
   ```
2. **Untuk mengakses alamat pertama dari karyawan pertama:**
   ```sql
   SELECT employee[OFFSET(0)].emp_address[OFFSET(0)].city FROM company WHERE company_name = 'Tech Innovators';
   ```
3. **Untuk mengakses email karyawan kedua:**
   ```sql
   SELECT employee[OFFSET(1)].emp_contact.email FROM company WHERE company_name = 'Tech Innovators';
   ```

   

