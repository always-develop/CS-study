# 02. ๋ฐ์ดํฐ

# [CS] ๐ฝ ํผ์ ๊ณต๋ถํ๋ ์ปดํจํฐ๊ตฌ์กฐ+์ด์์ฒด์ 

---

## 02. ๋ฐ์ดํฐ

### 02-1. 0๊ณผ 1๋ก ์ซ์๋ฅผ ํํํ๋ ๋ฐฉ๋ฒ

- ์ปดํจํฐ๊ฐ ์ดํดํ๋ ์ ๋ณด๋ 0๊ณผ 1, ๋นํธ(bit) ์ด๋ค
- 1024 ๋จ์๋ก ํํํ๋ ๋จ์๋ KiB, MiB, GiB, TiB ์ด๊ณ  ์๋๋ 1000 ๋จ์๊ฐ ๋ง๋ค๊ณ  ํ๋ค
- `์๋(word)`ย ๋?
  - CPU ๊ฐ ํ ๋ฒ์ ์ฒ๋ฆฌํ  ์ ์๋ ๋ฐ์ดํฐ ํฌ๊ธฐ
  - x86 CPU ๋ 32bit word, x64 CPU ๋ 64bit word ์ด๋ค
- ์ด์ง์์ ์ญ์ง์๋ฅผ ๊ตฌ๋ถํ๊ธฐ ์ํด ์ด์ง์์ ์๋์ฒจ์ย `(2)`ย ๋ฅผ ๋ถ์ด๊ฑฐ๋ ์์ย `0b`ย ๋ฅผ ๋ถ์ฌ ๊ตฌ๋ถํ๋ค
- ์์๋ฅผ ํํํ๊ธฐ ์ํด ๊ฐ์ฅ ๋ณดํธ์ ์ผ๋ก ์ฌ์ฉ๋๋ ๋ฐฉ๋ฒ์ 2์ ๋ณด์ ํ๊ธฐ๋ฒ์ด๋ค
  - `2์ ๋ณด์`ย ๋? ์ด๋ค ์๋ฅผ ๊ทธ๋ณด๋ค ํฐ 2n ์์ ๋บ ๊ฐ์ ์๋ฏธํ๋ค๊ณ  ํ๋ค
  - ์ฝ๊ฒ ๋งํ์๋ฉด ๋ชจ๋  0๊ณผ 1์ ๋ค์ง๊ณ  ๊ฑฐ๊ธฐ์ 1์ ๋ํ ๊ฐ์ด๋น!
- ํ์ง๋ง 2์ ๋ณด์๋ก ์ธํด ๋ณ๊ฒฝ๋ ์ด์ง์๋ ์ธ๋ป ๋ด์  ์์์ ์ด์ง์์ ๊ตฌ๋ถํ๊ธฐ ํ๋ค๋ค!
  - ๊ทธ๋ ๊ฒ ํ๊ธฐ ์ํด, ์ปดํจํฐ ๋ด๋ถ์์ ย `ํ๋๊ทธ`ย ๊ฐ์ ์ด์ฉํ์ฌ ์์์ ์์๋ฅผ ๊ตฌ๋ถํ๋ค
- 2์ ์ ๊ณฑ์ ๋ณด์๋ฅผ ์ทจํ๋ฉด ์๊ธฐ ์์ ์ด ๋์ด๋ฒ๋ฆฐ๋คโฆ!
  - ์๋ฅผ ๋ค์ด 8์ย `1000(2)`ย ์ธ๋ฐ, ์์ ํ๊ธฐ๋ย `1000(2)`ย ๊ฐ ๋์ด๋ฒ๋ฆฐ๋ค
  - ์ด๋ ๋ณธ์ง์ ์ธ ๋ฌธ์ ๋ก ํด๊ฒฐํ๊ธฐ ์ด๋ ต๋ค๊ณ  ํ๋ค
- ์ด์ง๋ฒ์ ๋๋ฌด ๊ธธ๊ธฐ ๋๋ฌธ์.. ์ญ์ก์ง๋ฒ๋ ์์ฃผ ์ฌ์ฉํ๋ค
- ์ญ์ก์ง์๋ ์๋์ฒจ์ย `(16)`ย ์ ์ฌ์ฉํ๊ฑฐ๋ย `0x`ย ๋ฅผ ๋ถ์ฌ ๊ตฌ๋ถํ๋ค
- ์ญ์ก์ง์๋ฅผ ์ด์ง์๋ก ๋ณํํ๋ ค๋ฉด, ์ญ์ก์ง์ ํ ๊ธ์๋ฅผ 4๋นํธ ์ด์ง์๋ก ๊ฐ์ฃผํ๋ฉด ๋๋ค๊ณ  ํ๋ค
- ๋ฐ๋๋ก ์ด์ง์๋ฅผ ์ญ์ก์ง์๋ก ๋ณํํ๋ ค๋ฉด ์ด์ง์ ์ซ์ ๋ค ๊ฐ๋ฅผ ๋์ด ํ๋์ ์ญ์ก์ง์๋ก ๋ณํํ๋ฉด ๋๋ค๊ณ  ํ๋ค

### 02-2. 0๊ณผ 1๋ก ๋ฌธ์๋ฅผ ํํํ๋ ๋ฐฉ๋ฒ

- ์ปดํจํฐ๊ฐ ์ธ์ํ๊ณ  ํํํ  ์ ์๋ ๋ฌธ์์ ๋ชจ์์ย `๋ฌธ์ ์งํฉ(Character set)`ย ์ด๋ผ๊ณ  ํ๋ค
  - ๋ฌธ์ ์งํฉ์ ์๋ ๋ฌธ์๋ ์ดํดํ  ์ ์๋ค
- ์ด ๋ฌธ์ ์งํฉ์ ์ํ ๋ฌธ์๋ค์ 0๊ณผ 1๋ก ๋ณํํ๊ธฐ ์ํ ๊ณผ์ ์ย `๋ฌธ์ ์ธ์ฝ๋ฉ(character encoding)`ย ์ด๋ผ๊ณ  ํ๋ค
- ๋ฐ๋๋ก, 0๊ณผ 1์ ๋ฌธ์ ์งํฉ์ ๋ฌธ์๋ก ๋ณํํ๋ ๊ณผ์ ์ย `๋ฌธ์ ๋์ฝ๋ฉ(character decoding)`ย ์ด๋ผ๊ณ  ํ๋ค
- `์์คํค(American Standard Code for Information Interchange, Ascii)`ย ๋ 0์ ์ ์ธํ๊ณ  7๋นํธ์ ์์ ๋ฒ์์ธ 127์ ๊ฐ์ง์๋ฅผ ํตํด ํํํ๋ ์ด์ฐฝ๊ธฐ์ ๋ฌธ์ ์งํฉ์ด๋ค
- Backspace, Escape, Cancel, Space ๊ฐ์ ์ ์ด ๋ฌธ์๋ ์์คํค ์ฝ๋์ ํฌํจ๋์ด์๋ค!
- ํ์ฅ ์์คํค๋ผ๋ ์ ๋ ์์ง๋ง, ์๋ 256๊ฐ์ ๋ฌธ์๋ง ํํํ  ์ ์๋ค
- ํ๊ธ ์ธ์ฝ๋ฉ์ ์์, ๋ชจ์, ๋ฐ์นจ ๊ฐ๊ฐ์ ๋ถ์ฌ๋ ์ฝ๋๋ฅผ ์กฐํฉํ์ฌ ๊ธ์๋ฅผ ๋ง๋๋ย `์กฐํฉํ ์ธ์ฝ๋ฉ`, ์กฐํฉ๋ ํ๋์ ๊ธ์์ ์ฝ๋๋ฅผ ๋ถ์ฌํ๋ย `์์ฑํ ์ธ์ฝ๋ฉ`ย ๋ฐฉ์์ด ์กด์ฌํ๋ค
- ํ๊ธ ์ธ์ฝ๋ฉ ๋ฐฉ์ย `EUC-KR`ย ์ ๋ํ์ ์ธ ์์ฑํ ์ธ์ฝ๋ฉ ๋ฐฉ์์ด๋ผ๊ณ  ํ๋ค
- EUC-KR ์๋ ์ ์๋์ง ์์ ๋ฌธ์์ด์ด ๋ง์๋ฐ, ์ ๊ฐ์๊ฑด ํํํ  ์ ์๋คใ 
- ํ๊ธ ๋ฟ๋ง ์๋๋ผ ๋ชจ๋  ๋๋ผ์ ๋ฌธ์๋ฅผ ํํํ๋ ์ธ์ฝ๋ฉ ๋ฐฉ์์ด ๋์กํด์, ๊ฒฐ๊ตญย `์ ๋์ฝ๋`ย ๋ผ๋ ํ์ค ๋ฌธ์ ์งํฉ์ด ๋ํ๋ฌ๋ค
  - ์ ๋์ฝ๋๋ ์์ฑํ ์ธ์ฝ๋ฉ ๋ฐฉ์์ ์ฌ์ฉํ์ฌ, ์์ฑ๋ ํ ๊ธ์๋ง๋ค ๊ณ ์ ์ ๊ฐ์ด ๋ถ์ฌ๋๋ ๋ฐฉ์์ ๋์ผํ์ง๋ง, ์ฝ๋๋ฅผ ๊ทธ๋๋ก ์ธ์ฝ๋ฉ ๊ฐ์ผ๋ก ์ผ๋ ๊ฒ์ด ์๋๋ผ, ์ฝ๋๋ฅผ ์ธ์ฝ๋ฉ ํ  ์ ์๋ ๋ฐฉ๋ฒ์ ๋ฐ๋ผ ๋ฌ๋ผ์ง๋ค
  - ์ ๋์ฝ๋๋ฅผ ์ธ์ฝ๋ฉํ๋ ๋ฐฉ๋ฒ์ด ๋ฐ๋กย `UTF-8`,ย `UTF-16`ย ๊ฐ์ ์ธ์ฝ๋ฉ์ด๋ผ๊ณ  ํ๋ค
- ํ๊ธ์ ์ ๋์ฝ๋๋ก ํํํ๋ค๋ฉดโฆ 3byte ๋ก ์ธ์ฝ๋ฉ๋๋ค
