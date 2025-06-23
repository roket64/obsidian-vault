### 컴파일 옵션
### 1. 방언(Dialect)

다음 옵션들을 통해 C-Family 언어(C++, Objective-C, Objective-C++)의 방언을 제어할 수 있습니다.

- `-ansi`: C언어에서 사용될 때 `-std=c90`, C++에서는 `-std=c++98`을 사용한 것과 같습니다.
- `-std=`: 언어 표준을 결정합니다. C 또는 C++ 컴파일러는 이 옵션만을 사용할 수 있습니다. 여기에 전달할 수 있는 인자는 다음과 같습니다.

	- `c90`, `c89`, `iso9899:1990`: ISO C90 프로그램 지원. 
	- `c99`, `iso9899:1999`: ISO C99.
	- `c11`, `iso9899:2011`: ISO C11.
	- `c17`, `c18`, `iso9899:2017`, `iso9899:2018`: ISO C17.
	- `c23`, `iso9899:2024`: ISO C23.
	- `c++98`, `c++03`: 1998 ISO C++ 표준.
	- `c++11`: 2011 ISO C++ 표준.
	- `c++14`: 2014 ISO C++ 표준.
	- `c++17`: 2017 ISO C++ 표준.
	- `c++20`: 2020 ISO C++ 표준.
	- `c++23`: 2023 ISO C++ 표준.
	- `gnu90`, `gnu89`: ISO C90의 GNU 방언.
	- `gnu99`: ISO C99의 GNU 방언.
	- `gnu11`: ISO C11의 GNU 방언.
	- `gnu17`, `gnu18`: ISO C17의 GNU 방언.
	- `gnu23`: ISO C23의 GNU 방언.
	- `gnu++98`: `std=c++98`의 GNU 방언.
	- `gnu++11`: `std=c++11`의 GNU 방언.
	- `gnu++14`: `std=c++14`의 GNU 방언.
	- `gnu++17`: `std=c++17`의 GNU 방언.
	- `gnu++20`: `std=c++20`의 GNU 방언.
	- `gnu++23`: `std=c++23`의 GNU 방언.

#### 2. 최적화

최적화 옵션을 적용하면 컴파일 시간을 컴파일 시간과 디버그 능력을 희생해 성능 및 코드 크기를 향상시킬 수 있습니다. 

- `-O0`: 기본 옵션이며, 최적화를 수행하지 않습니다. 컴파일 시간을 줄이고 디버깅이 가능하도록 합니다. 사용자에 의해 명시적으로 제공되는 최적화 옵션 또한 무시합니다.
- `-O, -O1`:  최적화합니다. 컴파일 시간과 메모리 사용 사이의 균형을 추구합니다. 이 옵션에 의해 활성화되는 옵션들은 다음과 같습니다.

	<details>
	<summary>활성화되는 옵션</summary>
	
	```
	-fauto-inc-dec
	-fbranch-count-reg
	-fcombine-stack-adjustments
	-fcompare-elim
	-fcprop-registers
	-fdce
	-fdefer-pop
	-fdelayed-branch
	-fdse
	-fforward-propagate
	-fguess-branch-probability
	-fif-conversion
	-fif-conversion2
	-finline-functions-called-once
	-fipa-modref
	-fipa-profile
	-fipa-pure-const
	-fipa-reference
	-fipa-reference-addressable
	-fivopts
	-fmerge-constants
	-fmove-loop-invariants
	-fmove-loop-stores
	-fomit-frame-pointer
	-freorder-blocks
	-fshrink-wrap
	-fshrink-wrap-separate
	-fsplit-wide-types
	-fssa-backprop
	-fssa-phiopt
	-ftree-bit-ccp
	-ftree-ccp
	-ftree-ch
	-ftree-coalesce-vars
	-ftree-copy-prop
	-ftree-dce
	-ftree-dominator-opts
	-ftree-dse
	-ftree-forwprop
	-ftree-fre
	-ftree-phiprop
	-ftree-pta
	-ftree-scev-cprop
	-ftree-sink
	-ftree-slsr
	-ftree-sra
	-ftree-ter
	-funit-at-a-time
	```
	</details>

- `-O2`: 더 최적화합니다. 공간을 희생하지 않는 거의 모든 최적화를 수행합니다. `-O1`에 의해 활성화되는 옵션에 더해 다음 옵션들을 활성화합니다.

	<details>
	<summary>활성화되는 옵션</summary>
	
	```
	-falign-functions  -falign-jumps
	-falign-labels  -falign-loops
	-fcaller-saves
	-fcode-hoisting
	-fcrossjumping
	-fcse-follow-jumps  -fcse-skip-blocks
	-fdelete-null-pointer-checks
	-fdevirtualize  -fdevirtualize-speculatively
	-fexpensive-optimizations
	-ffinite-loops
	-fgcse  -fgcse-lm
	-fhoist-adjacent-loads
	-finline-functions
	-finline-small-functions
	-findirect-inlining
	-fipa-bit-cp  -fipa-cp  -fipa-icf
	-fipa-ra  -fipa-sra  -fipa-vrp
	-fisolate-erroneous-paths-dereference
	-flra-remat
	-foptimize-crc
	-foptimize-sibling-calls
	-foptimize-strlen
	-fpartial-inlining
	-fpeephole2
	-freorder-blocks-algorithm=stc
	-freorder-blocks-and-partition  -freorder-functions
	-frerun-cse-after-loop
	-fschedule-insns  -fschedule-insns2
	-fsched-interblock  -fsched-spec
	-fstore-merging
	-fstrict-aliasing
	-fthread-jumps
	-ftree-builtin-call-dce
	-ftree-loop-vectorize
	-ftree-pre
	-ftree-slp-vectorize
	-ftree-switch-conversion  -ftree-tail-merge
	-ftree-vrp
	-fvect-cost-model=very-cheap
	```
	</details>

- `-O3`: 더더욱 최적화합니다. `-O2` 옵션에 더해 다음 옵션들을 활성화합니다. 

	<details>
	<summary>활성화되는 옵션</summary>
	
	```
	-fgcse-after-reload
	-fipa-cp-clone
	-floop-interchange
	-floop-unroll-and-jam
	-fpeel-loops
	-fpredictive-commoning
	-fsplit-loops
	-fsplit-paths
	-ftree-loop-distribution
	-ftree-partial-pre
	-funswitch-loops
	-fvect-cost-model=dynamic
	-fversion-loops-for-strides
	```
	</details>

- `-Os`: 바이너리 크기를 최적화합니다. `-O2`에 의해 활성화되는 옵션을 다음을 제외하고 적용합니다.

```
-falign-functions  -falign-jumps
-falign-labels  -falign-loops
-fprefetch-loop-arrays  -freorder-blocks-algorithm=stc
```

- `-Oz`: 속도보다 크기에 집중하여 적극적인 최적화를 수행합니다. `-Os` 옵션과 같이 `-O2`의 일부 최적화 옵션을 적용합니다.
- `-Og`: 디버깅을 위한 `-fvar-tracking-assignment`, `-fvar-tracking` 옵션을 활성화하고 최적화를 수행합니다. `-O0`  옵션과 마찬가지로 명시적으로 제공된 최적화 옵션을 무시합니다. 
#### 3. 경고 및 오류

- `-w`: 모든 경고를 무시합니다.
- `-Wall`: 거의 모든 구문 구성에 대한 경고를 활성화합니다. 이 옵션에 의해 활성화되는 옵션들은 다음과 같습니다.

	<details>
	<summary>활성화되는 옵션</summary>
	
	```
	-Waddress
	-Waligned-new (C++, Objective-C++ 한정)
	-Warray-bounds=1 (-O2 옵션 사용 시에만 한정)
	-Warray-compare
	-Warray-parameter=2
	-Wbool-compare
	-Wbool-operation
	-Wc++11-compat  -Wc++14-compat  -Wc++17compat  -Wc++20compat
	-Wcatch-value (C++, Objective-C++ 한정)
	-Wchar-subscripts
	-Wclass-memaccess (C++, Objective-C++ 한정)
	-Wcomment
	-Wdangling-else
	-Wdangling-pointer=2
	-Wdelete-non-virtual-dtor (C++, Objective-C++ 한정)
	-Wduplicate-decl-specifier (C, Objective-C 한정)
	-Wenum-compare  (C, ObjC 한정; C++는 기본으로 활성화되어있습니다.)
	-Wenum-int-mismatch (C, Objective-C 한정)
	-Wformat=1
	-Wformat-contains-nul
	-Wformat-diag
	-Wformat-extra-args
	-Wformat-overflow=1
	-Wformat-truncation=1
	-Wformat-zero-length
	-Wframe-address
	-Wimplicit (C, Objective-C 한정)
	-Wimplicit-function-declaration (C, Objective-C 한정)
	-Wimplicit-int (C, Objective-C 한정)
	-Winfinite-recursion
	-Winit-self (C++, Objective-C++ 한정)
	-Wint-in-bool-context
	-Wlogical-not-parentheses
	-Wmain (C, Objective-C 한정; -ffreestanding 옵션이 없을 경우 한정)
	-Wmaybe-uninitialized
	-Wmemset-elt-size
	-Wmemset-transposed-args
	-Wmisleading-indentation (C, C++ 한정)
	-Wmismatched-dealloc
	-Wmismatched-new-delete (C++, Objective-C++ 한정)
	-Wmissing-attributes
	-Wmissing-braces (C, Objective-C 한정)
	-Wmultistatement-macros
	-Wnarrowing  (C++, Objective-C++ 한정)
	-Wnonnull
	-Wnonnull-compare
	-Wopenmp-simd (C, C++ 한정)
	-Woverloaded-virtual=1 (C++, Objective-C++ 한정)
	-Wpacked-not-aligned
	-Wparentheses
	-Wpessimizing-move (C++, Objective-C++ 한정)
	-Wpointer-sign (C, Objective-C 한정)
	-Wrange-loop-construct (C++, Objective-C++ 한정)
	-Wreorder (C++, Objective-C++ 한정)
	-Wrestrict
	-Wreturn-type
	-Wself-move (C++, Objective-C++ 한정)
	-Wsequence-point
	-Wsign-compare (C++, Objective-C++ 한정)
	-Wsizeof-array-div
	-Wsizeof-pointer-div
	-Wsizeof-pointer-memaccess
	-Wstrict-aliasing
	-Wstrict-overflow=1
	-Wswitch
	-Wtautological-compare
	-Wtrigraphs
	-Wuninitialized
	-Wunknown-pragmas
	-Wunused
	-Wunused-but-set-variable
	-Wunused-const-variable=1 (C, Objective-C 한정)
	-Wunused-function
	-Wunused-label
	-Wunused-local-typedefs
	-Wunused-value
	-Wunused-variable
	-Wuse-after-free=2
	-Wvla-parameter
	-Wvolatile-register-var
	-Wzero-length-bounds
	```
	</details>

- `-Werror`: 발생하는 모든 경고를 오류로 취급합니다.
- `-Werror=`: 특정 경고를 컴파일 오류로 취급합니다. (가령, `-Werror=swith`는 `-Wswitch`에 의한 경고를 컴파일 오류로 취급합니다.)
- `-Wextra`: `-Wall` 옵션에 의해 활성화되지 않는 일부 옵션을 활성화합니다. 이때 활성화되는 옵션들은 다음과 같습니다.

	<details>
	<summary>활성화되는 옵션</summary>
	
	```
	-Wabsolute-value (C, Objective-C 한정)
	-Walloc-size
	-Wcalloc-transposed-args
	-Wcast-function-type
	-Wclobbered
	-Wdangling-reference (C++ 한정)
	-Wdeprecated-copy (C++, Objective-C++ 한정)
	-Wempty-body
	-Wenum-conversion (C, Objective-C 한정)
	-Wexpansion-to-defined
	-Wignored-qualifiers  (C, C++ 한정)
	-Wimplicit-fallthrough=3
	-Wmaybe-uninitialized
	-Wmissing-field-initializers
	-Wmissing-parameter-name (C, Objective-C 한정)
	-Wmissing-parameter-type (C, Objective-C 한정)
	-Wold-style-declaration (C, Objective-C 한정)
	-Woverride-init (C, Objective-C 한정)
	-Wredundant-move (C++, Objective-C++ 한정)
	-Wshift-negative-value ( C++11, C++17, C99 이상의 버전에 한정)
	-Wsign-compare (C++, Objective-C++ 한정)
	-Wsized-deallocation (C++, Objective-C++ 한정)
	-Wstring-compare
	-Wtype-limits
	-Wuninitialized
	-Wunterminated-string-initialization
	-Wunused-parameter (-Wunused 또는 -Wall 옵션과 사용될 때 한정)
	-Wunused-but-set-parameter (-Wunused 또는  -Wall 옵션과 사용될 때 한정)
	```
	</details>

- `-Wfatal-error`: 컴파일 오류가 발생했을 때 즉시 컴파일을 중단하며, 추가적인 오류 메세지를 출력하려고 시도하지 않습니다.
- `-Wpedantic, -pedantic`: [ISO C](https://www.iso.org/standard/82075.html), [ISO C++](https://www.iso.org/standard/83626.html) 에서 요구하는 모든 경고를 활성화하고, 금지된 확장을 사용하는 모든 프로그램과 표준을 따르지 않는 일부 다른 프로그램을 진단합니다.
- `-Wpedantic-error`: `-Wpedantic`옵션 등에 의해 진단이 요구되는 상황에 컴파일 오류를 발생시킵니다.

>[!INFO]
> `-Wpedantic-error`는 `-Werror=pedantic`과 동일하게 동작하지 않습니다. `-Wpedantic-error`는 `-Wpedantic`이외의 옵션에 의해 제어되는 다른 필수적인 진단에도 영향을 줄 수 있습니다. 

