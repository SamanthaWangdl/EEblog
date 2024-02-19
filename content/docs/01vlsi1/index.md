---
title: "VlSI1回顾: FPGA组成 与 Dedicated Processor 架构"
date: 2024-02-07
draft: false
description: "Discover what's new in Blowfish version 2.0."
tags: ["new", "docs"]
---

刚刚一学期上了VLSI1，课后配着systemverilog的一个HDMI的实验。这篇文章整理下这门课的一些要点。



## FPGA

![](https://raw.githubusercontent.com/SamanthaWangdl/imagehub/main/imagehub/screenshot0203.png)

- FPGA main component：LUT FF wire I/O
  - Plus: BRAM, CMT(clk management tile), DSP![Screenshot 2024-02-08 at 10.24.23](https://raw.githubusercontent.com/SamanthaWangdl/imagehub/main/imagehub/Screenshot%202024-02-08%20at%2010.24.23.png)



- FPGA 实现流程

![Screenshot 2024-02-08 at 10.24.56](https://raw.githubusercontent.com/SamanthaWangdl/imagehub/main/imagehub/Screenshot%202024-02-08%20at%2010.24.56.png)

## 系统设计优化方法

Goal of architecture design

- **functionality**
- **throughput**
- **production costs**
- **circuit size**
- **energy efficiency**



what algorithm suitable for vlsi architecture

1. **Loose coupling between major processing tasks.**
2. **Simple control flow.**
3. **Regular data flow.**
4. **Reasonable storage requirements**
5. **Compatible with finite precision arithmetics.**
6. **Non-recursive linear time-invariant computation.**
7. **No transcendental functions.**
8. **Extensive usage of data operations unavailable from standard instruction sets.**
9. **No divisions and multiplications on very wide data words, no matrix inversions.**
10. **Throughput rather than latency is what matters.**

### dedicated processor 

![Screenshot 2024-02-08 at 10.48.16](https://raw.githubusercontent.com/SamanthaWangdl/imagehub/main/imagehub/Screenshot%202024-02-08%20at%2010.48.16.png)





### Metrics

- longest path delay tlp
- Time per data item T
- data throughput
- Latency  L
- Circuit size A
- size-time product AT
- Energy per data item W/GOops

### Transform



![Screenshot 2024-02-08 at 10.58.01](https://raw.githubusercontent.com/SamanthaWangdl/imagehub/main/imagehub/Screenshot%202024-02-08%20at%2010.58.01.png)

- 优化从组合时序和存储三方面考虑
- 流水线的正确保证是割集



## SystemVerilog 硬件建模

- ETH 强调的 systemverilog 写法样本 
  - 三段式状态机


```systemverilog
module x_counter #(
    parameter integer XResolution,
    parameter integer XNumSections
) (
    input  logic    clk_i,
    input  logic    rst_ni,

    input  logic    valid_i,
    input  logic    ready_i,
    input  logic    hsync_i,
    input  logic    vde_i,

    output logic    x_edge_o
);

    logic [31:0]    x_count_d,  x_count_q;
    logic           x_edge_d,   x_edge_q;

    assign x_edge_o = x_edge_q;

    always_comb begin
        x_edge_d    = 1'b0;
        x_count_d   = x_count_q;
        if (valid_i && ready_i) begin // Only evaluate `hsync_i` and `vde_i` on handshakes.
            if (hsync_i) begin
                x_count_d = '0;
            end else if (vde_i) begin
                x_count_d = x_count_q + 1;
                if (x_count_q == (XResolution / XNumSections-1)) begin
                    x_count_d   = '0;
                    x_edge_d    = 1'b1;
                end
            end
        end
    end

    always_ff @(posedge clk_i, negedge rst_ni) begin
        if (!rst_ni) begin
            x_count_q   <= '0;
            x_edge_q    <= 1'b0;
        end else begin
            x_count_q   <= x_count_d;
            x_edge_q    <= x_edge_d;
        end
    end

endmodule

```



## SystemVerilog 验证

- assertion
- 标准验证代码的写法

```systemverilog
`timescale 1ns/1ns
module top;
	parameter int --;
	logic rst, clk;
	initial begin
		rst = 0; clk = 0;
		#5ns rst =1;
		#5ns clk = 1;
		#5ns clk =0;
	end
	fsm #( ) i_fsm();
	test #( ) i_test();
```



## Reference

1. top down 那本教材
2. lab note
3. hdlbits
