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
