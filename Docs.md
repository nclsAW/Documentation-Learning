# 🧪 Unit Testing dengan TypeScript

Unit testing adalah proses menguji **unit terkecil** dari sebuah program (fungsi/method) secara terisolasi, memastikan ia bekerja sesuai yang diharapkan.

Framework: **Jest** + **ts-jest** atau **Vitest** (built-in TypeScript support).

---

## Setup TypeScript

```bash
# Jest + ts-jest
npm install -D jest ts-jest @types/jest typescript
npx ts-jest config:init

# Atau pakai Vitest (lebih simpel, no config)
npm install -D vitest
```

```json
// tsconfig.json (minimal)
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "strict": true,
    "types": ["jest"]
  }
}
```

---

## Komponen Utama

### `describe`
Mengelompokkan test yang berkaitan ke dalam satu blok bernama. Bisa di-nest.

```ts
describe('Kalkulator', () => {
  describe('operasi dasar', () => {
    // test-test di sini
  })
})
```

---

### `test` / `it`
Mendefinisikan satu skenario pengujian. Keduanya **identik** secara fungsi.
- `test` → lebih eksplisit
- `it` → lebih natural: *"it should..."*

```ts
test('mengembalikan hasil penjumlahan', () => { ... })
it('should return the correct sum', () => { ... })
```

---

### `expect`
Titik awal assertion — di-chain dengan **matcher** untuk membandingkan nilai aktual vs yang diharapkan.

```ts
expect(tambah(2, 3)).toBe(5)
expect(user).toEqual({ id: 1, nama: 'Budi' })
expect(() => riskyFn()).toThrow()
```

---

### Matchers

| Matcher | Kegunaan |
|---|---|
| `toBe(val)` | Perbandingan ketat `===` (primitif) |
| `toEqual(val)` | Perbandingan dalam — untuk objek/array |
| `toStrictEqual(val)` | Seperti toEqual tapi lebih ketat (cek `undefined` property) |
| `toBeTruthy()` | Nilai truthy |
| `toBeFalsy()` | Nilai falsy |
| `toBeNull()` | Nilainya `null` |
| `toBeUndefined()` | Nilainya `undefined` |
| `toBeDefined()` | Bukan `undefined` |
| `toBeInstanceOf(Class)` | Instance dari suatu class |
| `toContain(item)` | Array/string mengandung item |
| `toHaveLength(n)` | Panjang array/string = n |
| `toHaveProperty(key, val?)` | Objek punya property tertentu |
| `toThrow(msg?)` | Fungsi melempar error |
| `toBeGreaterThan(n)` | Nilai lebih besar dari n |
| `toBeLessThan(n)` | Nilai lebih kecil dari n |
| `toBeCloseTo(n)` | Perbandingan float (hindari presisi desimal JS) |
| `toHaveBeenCalled()` | Mock function dipanggil |
| `toHaveBeenCalledTimes(n)` | Dipanggil sebanyak n kali |
| `toHaveBeenCalledWith(...args)` | Dipanggil dengan argumen tertentu |

---

### `beforeEach` / `afterEach`
Dijalankan **sebelum/sesudah setiap** test. Ideal untuk reset state atau inisialisasi ulang variabel.

```ts
let cart: ShoppingCart

beforeEach(() => {
  cart = new ShoppingCart() // fresh instance tiap test
})

afterEach(() => {
  jest.clearAllMocks() // reset mock call count
})
```

---

### `beforeAll` / `afterAll`
Dijalankan **sekali** di awal/akhir seluruh blok `describe`. Cocok untuk setup mahal seperti koneksi database.

```ts
let db: Database

beforeAll(async () => {
  db = await connectDB('test_db')
})

afterAll(async () => {
  await db.disconnect()
})
```

**Urutan eksekusi:**
```
beforeAll → beforeEach → test 1 → afterEach → beforeEach → test 2 → afterEach → afterAll
```

---

### `jest.fn()` — Mock Function
Membuat fungsi tiruan untuk menggantikan dependency eksternal. Bisa melacak panggilan, argumen, dan return value.

```ts
// TypeScript: tentukan signature-nya
const mockLog = jest.fn<(val: number) => void>()
const mockFetch = jest.fn<() => Promise<User>>()

// Set return value
mockFetch.mockResolvedValue({ id: 1, nama: 'Budi' })

// Assertions
expect(mockLog).toHaveBeenCalled()
expect(mockLog).toHaveBeenCalledTimes(1)
expect(mockLog).toHaveBeenCalledWith(42)
```

---

### `jest.spyOn()` — Spy
Memata-matai method yang sudah ada tanpa menggantinya sepenuhnya. Masih memanggil implementasi asli kecuali di-override.

```ts
const spy = jest.spyOn(console, 'log')
spy.mockImplementation(() => {}) // override sementara (opsional)

// ... jalankan kode yang pakai console.log ...

expect(spy).toHaveBeenCalledWith('pesan tertentu')
spy.mockRestore() // kembalikan implementasi asli
```

---

### `jest.mock()` — Module Mock
Mengganti seluruh modul dengan versi mock. Pakai `jest.mocked()` untuk type-safe di TypeScript.

```ts
jest.mock('axios') // harus di atas, sebelum import

import axios from 'axios'

const mockedAxios = jest.mocked(axios) // type-safe helper
mockedAxios.get.mockResolvedValue({ data: { nama: 'Budi' } })
```

---

### `skip` & `only`
- `test.skip` / `it.skip` → lewati test sementara
- `test.only` / `it.only` → hanya jalankan test ini (berguna saat debug)

```ts
test.skip('fitur ini belum diimplementasi', () => { ... })
test.only('hanya ini yang jalan sekarang', () => { ... })
```

> ⚠️ Jangan lupa hapus `.only` sebelum commit — bisa bikin CI hanya jalan 1 test!

---

## Contoh Lengkap (TypeScript)

```ts
// types/kalkulator.ts
export interface HasilOperasi {
  nilai: number
  operasi: string
  timestamp: Date
}

// utils/kalkulator.ts
import type { HasilOperasi } from '../types/kalkulator'

export function bagi(a: number, b: number): HasilOperasi {
  if (b === 0) throw new Error('Tidak bisa bagi dengan nol')
  return {
    nilai: a / b,
    operasi: `${a} / ${b}`,
    timestamp: new Date()
  }
}

export function kali(a: number, b: number): number {
  return a * b
}
```

```ts
// utils/kalkulator.test.ts
import { bagi, kali } from './kalkulator'
import type { HasilOperasi } from '../types/kalkulator'

// describe → kelompokkan semua test kalkulator
describe('Kalkulator', () => {

  // afterEach → reset mock setelah tiap test
  afterEach(() => {
    jest.clearAllMocks()
  })

  describe('bagi()', () => {

    // it → skenario sukses, cek HasilOperasi
    it('mengembalikan HasilOperasi yang benar', () => {
      const hasil: HasilOperasi = bagi(10, 2)

      expect(hasil.nilai).toBe(5)                  // toBe: primitif
      expect(hasil.operasi).toContain('10')         // toContain: substring
      expect(hasil.nilai).toBeGreaterThan(0)        // toBeGreaterThan
      expect(hasil.timestamp).toBeInstanceOf(Date)  // toBeInstanceOf
    })

    // test → skenario error, toThrow
    test('melempar Error saat dibagi nol', () => {
      expect(() => bagi(10, 0))
        .toThrow('Tidak bisa bagi dengan nol')
    })
  })

  describe('kali() + mock logger', () => {

    // jest.fn() → mock dengan TypeScript type
    it('memanggil logger dengan hasil perkalian', () => {
      const logger = {
        log: jest.fn<(val: number) => void>()
      }

      function kaliDanLog(a: number, b: number): number {
        const hasil = kali(a, b)
        logger.log(hasil)
        return hasil
      }

      const hasil = kaliDanLog(3, 4)

      expect(hasil).toBe(12)                         // hasil benar
      expect(logger.log).toHaveBeenCalledTimes(1)    // dipanggil 1x
      expect(logger.log).toHaveBeenCalledWith(12)    // dengan nilai 12
    })
  })

  // test.skip → dilewati sementara
  test.skip('fitur modulo belum diimplementasi', () => {
    expect(true).toBe(false)
  })
})
```

**Output yang diharapkan:**
```
PASS utils/kalkulator.test.ts
  Kalkulator
    bagi()
      ✓ mengembalikan HasilOperasi yang benar
      ✓ melempar Error saat dibagi nol
    kali() + mock logger
      ✓ memanggil logger dengan hasil perkalian
    ○ fitur modulo belum diimplementasi (skipped)
```

---

## Ringkasan Cepat

```
describe          → wadah/grup test
it / test         → satu skenario test
expect            → nilai yang mau dicek
matchers          → cara ngeceknya (toBe, toEqual, toThrow, dll)
beforeEach        → setup sebelum tiap test (paling sering dipakai)
afterEach         → cleanup setelah tiap test
beforeAll/afterAll → setup/cleanup sekali untuk seluruh suite
jest.fn<T>()      → mock function dengan TypeScript type
jest.mocked()     → type-safe wrapper untuk module mock
spyOn             → awasi/override method yang sudah ada
.skip             → lewatin test sementara
.only             → jalanin test ini aja (jangan lupa dihapus!)
```
