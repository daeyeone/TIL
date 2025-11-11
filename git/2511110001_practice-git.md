1. `github`에서 새로운 repo를 생성합니다(이름:자유, public, README.md 활성화, MIT LICENSE)
2. `~/Documents/dev/` 에서 repo를 clone합니다. `.gitignore`를 만들고 본인의 환경에 맞는 ignore 설정을 합니다.

```shell
$ git clone {addr}
$ cd {repo-name}
$ touch .gitignore
$ vi .gitignore
```

3. 새 브랜치를 만듭니다.(이름: `fibo-rec`)

3-1. fibo-rec 브랜치로 이동하여, 점화식으로 fibonacci sequence를 구현합니다.(새 파일: `fibo-seq.py`)

```python
def fibo(n):
    if n < 2:
        return n
    else:
        fibo(n - 1) + fibo(n - 2)
```

3-2. git `add, commit, push` 한 뒤, pull request를 이용하여 `github`에서 remote의 main에 merge 합니다.

3-3. local의 main에 update된 remote의 main을 `fetch & merge` 합니다.

```shell
# 브랜치 생성하고 들어가서 작업하기
$ git branch fibo-rec
$ git switch fibo-rec
$ touch fibo-seq.py

$ vi fibo-seq.py
# 작업 후 remote(github)에 업로드하기
$ git add fibo-seq.py
$ git commit -m "feat: Do Fibo with recursion"
$ git push -u origiin fibo-rec
# Pull Request 절차 마무리 후 local의 main 업데이트하기
$ git switch main
$ git fetch origin main
$ git merge FETCH_HEAD
```

4. 새 브랜치를 만듭니다.(이름: `fibo-mem`)

4-1. `fibo-mem` 브랜치로 이동하여, memoization을 적용한 fibonacci sequence를 구현합니다. (fibo-seq.py에서 바로 작업)

```python
def fibo(n):
	pad = {0: 0, 1: 1}
	def fib_inner(n):
		if n not in pad:
			pad[n] = fib_inner(n - 1) + fib_inner(n - 2)
		return pad[n]
	return fib_inner(n)


if __name__ == '__main__':
    print(fibo(4))
```

4-2. git add, commit, push 한 뒤, pull request를 이용하여 `github`에서 remote의 main에 merge 합니다.

4-3. local의 main에 update된 remote의 main을 fetch & merge 합니다.

5. 새 브랜치를 만듭니다.(이름: `fibo-binet`)

5-1. `fibo-binet` 브랜치로 이동하여, binet의 공식을 활용하여 fibonacci sequence를 구현합니다. (fibo-seq.py에서 바로 작업)

```python
import math

def binet_fibonacci(n):
  """
  Binet의 공식을 사용하여 n번째 피보나치 수를 계산합니다.
  """
  phi = (1 + math.sqrt(5)) / 2
  # psi = (1 - math.sqrt(5)) / 2 # psi 항은 매우 작아져서, n이 클 경우 0으로 수렴합니다.
  # 따라서 아래와 같이 간단하게 계산할 수 있습니다.
  result = (phi**n) / math.sqrt(5)
  return round(result)

# 예시
print(binet_fibonacci(10))

```

5-2. git `add, commit, push` 한 뒤, pull request를 이용하여 `github`에서 remote의 main에 merge 합니다.

5-3. local의 main에 update된 remote의 main을 `fetch & merge` 합니다.
