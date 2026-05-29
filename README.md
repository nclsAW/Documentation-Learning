# 📄 Ringkasan Kode

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

## Mocking Modul & Advanced Mocking
```
jest.mock('modul')          → mock satu modul full (package/file) secara otomatis
jest.requireActual('modul') → ambil fungsi asli dari modul yang sedang di-mock (Partial Mocking)
jest.doMock()               → mirip jest.mock, tapi bisa dijalankan di dalam blok kode (lazy/dynamic)
jest.dontMock() / unmock()  → pastiin modul tetep pakai yang asli (gak kena automock)
jest.isolateModules()       → jalankan test di dalam *sandbox* isolasi biar gak ngerusak cache module lain
```
## Mock Lifecycles & Resetting (Anti-Leak)
```
jest.clearAllMocks()        → hapus riwayat panggilan mock (toHaveBeenCalledTimes, dll) antar test
jest.resetAllMocks()        → hapus riwayat DAN reset implementasi mock balik ke fungsi kosong
jest.restoreAllMocks()      → kembalikan fungsi yang di-spyOn balik ke fungsi bawaan aslinya
afterEach(() => {})         → tempat paling wajib buat naruh clear/reset mock biar gak bocor
```
## Advanced Matchers (Object & String/Array)
```
expect.stringMatching(regex) → cek apakah string cocok dengan pola Regex tertentu
expect.stringContaining(str) → cek apakah string mengandung potongan kata tertentu (loose check)
expect.arrayContaining([x])  → cek apakah array mengandung elemen x, gak peduli urutan/indeksnya
toHaveProperty('a.b.c', val) → cek deep property/nested object tanpa takut error undefined
toContainEqual(obj)          → mirip .toContain, tapi khusus buat nyari object di dalam array
```
## Timer Control (Pake Fake Timers)
```
jest.advanceTimersByTime(ms) → "percepat waktu" sekian milidetik buat ngetest setTimeout/setInterval
jest.runAllTimers()          → langsung eksekusi semua antrean timer yang sedang berjalan
jest.runOnlyPendingTimers()  → eksekusi timer yang saat ini sedang menggantung aja
```

## Custom & Utilities
```
expect.extend({ matcher })   → bikin fungsi matcher buatan sendiri (custom assertion)
jest.retryTimes(number)      → ulangi test yang gagal otomatis beberapa kali (buat e2e/integration)
```
