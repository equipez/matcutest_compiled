# MatCUTEst (compiled)

[![CI](https://github.com/equipez/matcutest_compiled/actions/workflows/ci.yml/badge.svg)](https://github.com/equipez/matcutest_compiled/actions/workflows/ci.yml)

## What is this?

This is a compiled version of [MatCUTEst](https://github.com/equipez/matcutest), which aims to facilitate the usage of [CUTEst](https://github.com/ralna/CUTEst) in MATLAB on **Linux**.

## How to install?

Before starting, make sure that [`7-Zip`](https://en.wikipedia.org/wiki/7-Zip) is installed
(e.g., try `type 7z || sudo apt install p7zip-full` on Ubuntu).

### Brief version

```
git clone https://github.com/equipez/matcutest_compiled.git && matlab -batch "cd matcutest_compiled; install;" && rm -rf matcutest_compiled
```

### Detailed version

1. Clone this repository. You should then get a folder containing this README file the
[`install.m`](install.m) file.

2. In the command window of MATLAB, change your directory to the above-mentioned folder, and execute

```
install
```

You may specify the path where you want MatCUTEst to be installed by passing it as an input to `install`.

If the above succeeds, then the [CUTEst](https://github.com/ralna/CUTEst) problems should be
available to you via `macup`, `secup`, etc. Try `help matcutest` for more information.

Success is expected if you are using [MATLAB R2020a or
above on Ubuntu 20.04 or above](https://github.com/equipez/matcutest_compiled/actions/workflows/ci.yml).
Let me know by opening an issue if this is not the case.

If this compiled version does not work, then you may try installing
[MatCUTEst](https://github.com/equipez/matcutest) from source
following the [README](https://github.com/equipez/matcutest/blob/main/README.md) therein.


## Use MatCUTEst in GitHub Actions

If you want to use MatCUTEst in [GitHub Actions](https://docs.github.com/en/actions), see
the [demo](https://github.com/equipez/matcutest_compiled/blob/main/.github/workflows/demo.yml).
MatCUTEst has been used intensively in the testing and development of [PRIMA](http://www.libprima.net),
where you can find more [realistic examples](https://github.com/libprima/prima/blob/main/.github/workflows/verify_large.yml)
of using MatCUTEst in GitHub Actions.


## Thread safety

MatCUTEst is [thread-safe](https://en.wikipedia.org/wiki/Thread_safety). It can be used within
a [`parfor` ](https://www.mathworks.com/help/parallel-computing/parfor.html). Here is an example.

```
problist = {'AKIVA', 'BOX2', 'ZECEVIC2', 'ZY2'};
parfor ip = 1 : length(problist)
    pname = problist{ip};
    fprintf('\n%d. Try %s:\n', ip, pname);
    p = macup(pname);  % make a CUTEst problem
    p.objective(p.x0)
    decup(p);  % destroy the CUTEst problem
end
```


## Remarks

- MatCUTEst has been playing a vital role in the testing and development of [PRIMA](http://www.libprima.net).
- If you would like to use CUTEst in Python, check [PyCUTEst](https://github.com/jfowkes/pycutest).
