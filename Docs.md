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

# 🧪 Unit Testing TypeScript — Tambahan & Pelengkap

> Dokumen ini melanjutkan referensi utama. Semua yang ada di bawah **belum tercakup** di dokumen sebelumnya.

---

## Alias Skip yang Lebih Pendek: `xit` / `xtest` / `xdescribe`

Selain `.skip`, Jest/Vitest juga punya versi prefix `x` yang bekerja **identik** — cukup tambahkan `x` di depan.

```ts
// Semua ini setara dengan .skip:
xit('belum diimplementasi', () => { ... })       // = it.skip(...)
xtest('belum diimplementasi', () => { ... })     // = test.skip(...)
xdescribe('modul belum siap', () => { ... })     // = describe.skip(...)
```

> 💡 `xit` berasal dari konvensi Jasmine (framework lama). Jest/Vitest mempertahankannya untuk kompatibilitas. Pilih satu gaya dan konsisten.

---

## `test.todo` — Tandai Test yang Belum Ditulis

Berbeda dengan `.skip` yang meng-skip test yang sudah ada, `.todo` dipakai untuk **mendaftarkan test yang belum ditulis sama sekali**. Tidak boleh ada callback.

```ts
test.todo('validasi email harus reject format tanpa @')
test.todo('refresh token otomatis setelah expired')
```

Output di terminal:
```
  ✎ todo  validasi email harus reject format tanpa @
  ✎ todo  refresh token otomatis setelah expired
```

> Cocok dipakai saat planning — tulis dulu test-test apa yang perlu dibuat, implementasi belakangan.

---

## `test.each` / `it.each` — Parameterized Tests

Menjalankan test yang sama dengan **banyak input berbeda**, tanpa duplikasi kode.

### Gaya Array of Arrays

```ts
test.each([
  [1, 1, 2],
  [2, 3, 5],
  [0, -1, -1],
])('tambah(%i, %i) = %i', (a, b, expected) => {
  expect(tambah(a, b)).toBe(expected)
})
```

### Gaya Array of Objects (lebih readable, TypeScript-friendly)

```ts
interface KasusUji {
  a: number
  b: number
  expected: number
}

test.each<KasusUji>([
  { a: 1, b: 1, expected: 2 },
  { a: 2, b: 3, expected: 5 },
  { a: 0, b: -1, expected: -1 },
])('tambah($a, $b) harus $expected', ({ a, b, expected }) => {
  expect(tambah(a, b)).toBe(expected)
})
```

### Gaya Tagged Template Literal

```ts
it.each`
  a     | b     | expected
  ${1}  | ${1}  | ${2}
  ${2}  | ${3}  | ${5}
  ${0}  | ${-1} | ${-1}
`('tambah($a, $b) = $expected', ({ a, b, expected }) => {
  expect(tambah(a, b)).toBe(expected)
})
```

---

## `describe.each` — Suite Parameterized

Sama seperti `test.each` tapi untuk seluruh blok `describe`.

```ts
describe.each([
  { db: 'mysql', port: 3306 },
  { db: 'postgres', port: 5432 },
])('koneksi ke $db', ({ db, port }) => {
  it('terhubung di port yang benar', () => {
    expect(getDefaultPort(db)).toBe(port)
  })

  it('nama driver valid', () => {
    expect(getDriverName(db)).toBeTruthy()
  })
})
```

---

## `test.concurrent` — Paralel Test

Menjalankan test secara **paralel** (berguna untuk async yang lambat). Hati-hati dengan shared state.

```ts
describe('API calls', () => {
  test.concurrent('fetch user', async () => {
    const user = await fetchUser(1)
    expect(user.id).toBe(1)
  })

  test.concurrent('fetch posts', async () => {
    const posts = await fetchPosts()
    expect(posts).toHaveLength(10)
  })
})
```

> ⚠️ Jangan pakai `test.concurrent` kalau test saling berbagi state (variabel global, database tunggal, dll).

---

## `test.failing` — Expect-to-Fail

Kebalikan dari test biasa — test ini **dianggap berhasil kalau dia gagal**. Berguna untuk mendokumentasikan known bug.

```ts
test.failing('bug: bagi dengan -0 harusnya throw', () => {
  // ini harusnya throw, tapi belum — test ini akan PASS selama bug masih ada
  expect(() => bagi(5, -0)).toThrow()
})
```

> Kalau bug-nya diperbaiki dan test ini tiba-tiba pass, Jest akan menandainya sebagai failure — mengingatkan kamu untuk menghapus `.failing`.

---

## Async Testing

### Promise langsung

```ts
it('resolve dengan data user', () => {
  return fetchUser(1).then(user => {
    expect(user.name).toBe('Budi')
  })
})
```

### `async/await` (paling umum)

```ts
it('resolve dengan data user', async () => {
  const user = await fetchUser(1)
  expect(user.name).toBe('Budi')
})
```

### `resolves` / `rejects` matcher

```ts
// Lebih ringkas — langsung pada Promise-nya
it('resolve dengan nama Budi', async () => {
  await expect(fetchUser(1)).resolves.toMatchObject({ name: 'Budi' })
})

it('reject kalau user tidak ada', async () => {
  await expect(fetchUser(999)).rejects.toThrow('User not found')
})
```

> ⚠️ Selalu `await` saat pakai `.resolves`/`.rejects` — kalau lupa `await`, test bisa pass palsu.

---

## Matchers Tambahan yang Terlewat

| Matcher | Kegunaan |
|---|---|
| `toMatchObject(obj)` | Objek mengandung subset property (tidak harus persis sama) |
| `toMatchSnapshot()` | Bandingkan dengan snapshot yang tersimpan |
| `toMatchInlineSnapshot()` | Snapshot langsung di dalam kode test |
| `toStrictEqual(val)` | Seperti `toEqual` tapi lebih ketat — cek `undefined` property & class |
| `not.toBe(val)` | Negasi — bisa dipakai di depan matcher manapun |
| `expect.any(Constructor)` | Match nilai dari tipe apapun: `expect.any(Number)` |
| `expect.anything()` | Match nilai apapun kecuali `null`/`undefined` |
| `expect.arrayContaining([...])` | Array mengandung subset tertentu (urutan bebas) |
| `expect.objectContaining({...})` | Objek mengandung subset property tertentu |
| `expect.stringContaining(str)` | String mengandung substring |
| `expect.stringMatching(regex)` | String match regex |
| `toHaveBeenNthCalledWith(n, ...args)` | Panggilan ke-N mock menggunakan argumen tertentu |
| `toHaveBeenLastCalledWith(...args)` | Panggilan terakhir mock menggunakan argumen tertentu |
| `toHaveReturnedWith(val)` | Mock mengembalikan nilai tertentu |
| `toHaveLastReturnedWith(val)` | Panggilan terakhir mock mengembalikan nilai tertentu |

### Contoh `expect.objectContaining`

```ts
it('response mengandung field yang dibutuhkan', () => {
  const response = { id: 1, name: 'Budi', createdAt: new Date(), token: 'abc' }

  expect(response).toMatchObject(
    expect.objectContaining({
      id: expect.any(Number),
      name: expect.any(String),
    })
  )
})
```

---

## `jest.fn()` — Lanjutan

### `mockReturnValue` vs `mockResolvedValue`

```ts
const mockSync = jest.fn().mockReturnValue(42)              // sync
const mockAsync = jest.fn().mockResolvedValue({ id: 1 })    // async (Promise.resolve)
const mockReject = jest.fn().mockRejectedValue(new Error()) // async (Promise.reject)
```

### `mockReturnValueOnce` — Return berbeda tiap panggilan

```ts
const mockFetch = jest.fn()
  .mockResolvedValueOnce({ data: 'pertama' })   // panggilan ke-1
  .mockResolvedValueOnce({ data: 'kedua' })     // panggilan ke-2
  .mockResolvedValue({ data: 'default' })       // panggilan selanjutnya

await mockFetch() // { data: 'pertama' }
await mockFetch() // { data: 'kedua' }
await mockFetch() // { data: 'default' }
```

### `mockImplementation` — Implementasi kustom

```ts
const mockBagi = jest.fn().mockImplementation((a: number, b: number) => {
  if (b === 0) throw new Error('Tidak bisa bagi nol')
  return a / b
})
```

### Reset mock

```ts
mockFn.mockClear()   // reset call count & history (bukan implementasi)
mockFn.mockReset()   // reset semua + hapus implementasi/return value
mockFn.mockRestore() // kembalikan ke implementasi asli (khusus spyOn)
```

---

## `jest.spyOn()` — Lanjutan

```ts
// Spy pada method statis
const spy = jest.spyOn(MathUtils, 'round')
spy.mockReturnValue(10)

// Spy pada getter (properti)
const spy = jest.spyOn(obj, 'nama', 'get').mockReturnValue('Mock Nama')

// Spy pada setter
const spy = jest.spyOn(obj, 'nilai', 'set')
obj.nilai = 42
expect(spy).toHaveBeenCalledWith(42)
```

---

## `jest.useFakeTimers()` — Mock Waktu

Untuk test yang menggunakan `setTimeout`, `setInterval`, `Date`, dll.

```ts
describe('auto-logout setelah idle', () => {
  beforeEach(() => {
    jest.useFakeTimers()
  })

  afterEach(() => {
    jest.useRealTimers()
  })

  it('logout setelah 30 menit idle', () => {
    const logout = jest.fn()
    setupIdleTimer(logout)

    jest.advanceTimersByTime(30 * 60 * 1000) // skip waktu 30 menit

    expect(logout).toHaveBeenCalledTimes(1)
  })
})
```

| Method | Kegunaan |
|---|---|
| `jest.useFakeTimers()` | Aktifkan fake timer |
| `jest.useRealTimers()` | Kembali ke timer asli |
| `jest.advanceTimersByTime(ms)` | Maju waktu sejumlah ms |
| `jest.runAllTimers()` | Jalankan semua pending timer |
| `jest.runOnlyPendingTimers()` | Jalankan hanya timer yang sudah pending |
| `jest.setSystemTime(date)` | Set `Date.now()` ke nilai tertentu |

---

## Snapshot Testing

### `toMatchSnapshot()`

Pertama kali dijalankan → membuat file snapshot. Berikutnya → membandingkan.

```ts
it('render komponen dengan benar', () => {
  const tree = renderToString(<Button label="Simpan" />)
  expect(tree).toMatchSnapshot()
})
```

Untuk **update** snapshot setelah perubahan yang disengaja:
```bash
npx jest --updateSnapshot
# atau
npx jest -u
```

### `toMatchInlineSnapshot()` — Snapshot di dalam kode

```ts
it('format nama lengkap', () => {
  expect(formatNama('budi', 'santoso')).toMatchInlineSnapshot(`
    "Budi Santoso"
  `)
})
```

> Jest akan otomatis mengisi string di dalam backtick saat pertama kali dijalankan.

---

## Type-Level Testing dengan `expectTypeOf` (Vitest)

Khusus Vitest — untuk menguji **tipe TypeScript**, bukan nilai runtime.

```ts
import { expectTypeOf } from 'vitest'

it('tambah mengembalikan number', () => {
  expectTypeOf(tambah).returns.toBeNumber()
  expectTypeOf(tambah).parameters.toEqualTypeOf<[number, number]>()
})
```

---

## Ringkasan Tambahan

```
xit / xtest / xdescribe  → alias untuk .skip (gaya Jasmine)
test.todo                 → daftarkan test yang belum ditulis (no callback)
test.each / it.each      → parameterized test (banyak input, 1 test)
describe.each            → parameterized suite
test.concurrent          → jalankan test secara paralel
test.failing             → test yang diharapkan gagal (known bug)
.resolves / .rejects     → matcher untuk Promise (selalu await!)
toMatchObject            → cek subset property objek
expect.objectContaining  → flexible matcher untuk objek
expect.any(Constructor)  → flexible matcher untuk tipe
mockReturnValueOnce      → return value berbeda tiap panggilan
mockImplementation       → implementasi custom untuk mock
jest.useFakeTimers()     → mock setTimeout, Date, dll
toMatchSnapshot()        → snapshot testing
expectTypeOf (Vitest)    → type-level testing
```
