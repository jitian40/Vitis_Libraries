# Vitis Project for TPC-H Q5

## Overview

This project demostrate FPGA acceleration of TPC-H Q5 on scale factor 1 data.

```
select
        n_name,
        sum(l_extendedprice * (1 - l_discount)) as revenue
from
        customer,
        orders,
        lineitem,
        supplier,
        nation,
        region
where
        c_custkey = o_custkey
        and l_orderkey = o_orderkey
        and l_suppkey = s_suppkey
        and c_nationkey = s_nationkey
        and s_nationkey = n_nationkey
        and n_regionkey = r_regionkey
        and r_name = 'MIDDLE EAST'
        and o_orderdate >= date '1994-01-01'
        and o_orderdate < date '1995-01-01'
group by
        n_name
order by
        revenue desc
;
```

## Makefile Targets

  * data: prepare the test data.

  * run\_sw\_emu: software emulation.

  * run\_hw\_emu: hardware emulation.

  * run\_hw: execute on board.

## Dataset

We used the TPC-H dataset generated with ssb-dbgen tool.
The makefile will download the tool and create data files when processing the `data` target.

## Building Notes

Some environment variables have to be set before building the project:
```
bash $ source env.sh
```