<p align="center">
  <img src="https://gvinciguerra.github.io/PGM-index/images/logo.svg" alt="The PGM-index" style="width: 565px">
</p>

<p align="center">The Piecewise Geometric Model index (PGM-index) is a data structure that enables fast point and range searches in arrays of billions of items using orders of magnitude less space than traditional indexes.</p>

<p align="center">
    <a href="https://gvinciguerra.github.io/PGM-index" rel="nofollow" class="rich-diff-level-one">Website</a>
    | <a href="https://gvinciguerra.github.io/PGM-index/docs" rel="nofollow" class="rich-diff-level-one">Documentation</a>
    | <a href="https://arxiv.org/abs/1910.06169" rel="nofollow" class="rich-diff-level-one">Paper</a>
    | <a href="http://acube.di.unipi.it" rel="nofollow" class="rich-diff-level-one">A³ Lab</a></p>
</p>

<p align="center">
    <a href="https://travis-ci.org/gvinciguerra/PGM-index"><img src="https://img.shields.io/travis/gvinciguerra/PGM-index" alt="Travis (.org)"></a>
    <a href="https://github.com/gvinciguerra/PGM-index/blob/master/LICENSE" class="rich-diff-level-one"><img src="https://img.shields.io/github/license/gvinciguerra/PGM-index" alt="License"></a>
    <a href="https://github.com/gvinciguerra/PGM-index/stargazers" class="rich-diff-level-one"><img src="https://img.shields.io/github/stars/gvinciguerra/PGM-index" alt="GitHub stars"></a></p>
</p>

## Building the code

To download and build the library use the following commands:

```bash
git clone https://github.com/gvinciguerra/PGM-index.git
cd PGM-index
git submodule update --init --recursive
cmake . -DCMAKE_BUILD_TYPE=Release
make -j8
```

Now you can run the unit tests via:

```
./test/tests
```

## Minimal example

```cpp
#include <vector>
#include <cstdlib>
#include <iostream>
#include <algorithm>
#include "pgm_index.hpp"

int main(int argc, char **argv) {
    // Generate some random data
    std::vector<int> dataset(1000000);
    std::generate(dataset.begin(), dataset.end(), std::rand);
    dataset.push_back(42);
    std::sort(dataset.begin(), dataset.end());

    // Construct the PGM-index
    const int error = 128;
    PGMIndex<int, error> index(dataset);

    // Query the PGM-index
    auto q = 42;
    auto approx_range = index.find_approximate_position(q);
    auto lo = dataset.cbegin() + approx_range.lo;
    auto hi = dataset.cbegin() + approx_range.hi;
    std::cout << *std::lower_bound(lo, hi, q);

    return 0;
}
```

## License

This project is licensed under the terms of the GNU General Public License v3.0.

If you use the library please put a link to the [website](https://gvinciguerra.github.io/PGM-index) and cite the following paper:
```tex
@misc{FerraginaVinciguerra:2019,
  Archiveprefix = {arXiv},
  Author = {Paolo Ferragina and Giorgio Vinciguerra},
  Day = {14},
  Eprint = {1910.06169},
  Month = {10},
  Primaryclass = {cs.DS},
  Title = {The PGM-index: a multicriteria, compressed and learned approach to data indexing},
  Url = {https://arxiv.org/abs/1910.06169},
  Year = {2019}}
```
