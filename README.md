# Simple Epoch Based Memory Reclaimer

[![Build Status](https://dev.azure.com/haoxiangpeng/epoch-reclaimer/_apis/build/status/XiangpengHao.epoch-reclaimer?branchName=master)](https://dev.azure.com/haoxiangpeng/epoch-reclaimer/_build/latest?definitionId=1&branchName=master)

Code adapted from [PMwCAS](https://github.com/microsoft/pmwcas), all bugs are mine.

## Features

- Small, simple, feature-compelete

- Epoch Manager + Garbage List

- Header-only

## Build

```bash
mkdir build && cd build
cmake -DCMAKE_BUILD_TYPE={Debug|Release} ..
make tests
```

## Usage

```c++
struct MockItem {
 public:
  MockItem() {}

  static void Destroy(void* destroyContext, void* p) {
    // some complex memory cleanup
  }
};


EpochManager epoch_manager_;
epoch_manager_.Initialize()

GarbageList garbage_list_;
// 1024 is the number of addresses that can be held aside for pointer stability.
garbage_list_.Initialize(&epoch_manager_, 1024);

// MockItem::Destory is the deallocation callback
garbage_list_.Push(new MockItem(), MockItem::Destroy, nullptr);
garbage_list_.Push(new MockItem(), MockItem::Destroy, nullptr);
```


