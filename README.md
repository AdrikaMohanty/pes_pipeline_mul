# pes_pipeline_mul
<details>
   <summary>GLS </summary>

The design chosen here is a pipelined multiplier 

### Before synthesis RTL :

![image](https://github.com/AdrikaMohanty/pes_pipeline_mul/assets/84654826/7cc8fb57-78a6-4130-a6f2-7f6f01b0dc5b)


for synthesis use the following command :

``` read_liberty -lib /home/adrika/vsd/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib```


![image](https://github.com/AdrikaMohanty/pes_pipeline_mul/assets/84654826/7dd920bd-37cf-41b3-ae04-f05dcc81dc3f)



```
    read_verilog /home/adrika/vsd/assignment/pes_pipeline_mul.v
    synth -top pes_pipeline_mul
```



![image](https://github.com/AdrikaMohanty/pes_pipeline_mul/assets/84654826/91239de8-8cde-4dd9-b401-368b0d988f04)


``` abc -liberty /home/adrika/vsd/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib   ```


abc results :

![image](https://github.com/AdrikaMohanty/pes_pipeline_mul/assets/84654826/3516c770-4257-470d-8bbb-0f33870940ae)


![image](https://github.com/AdrikaMohanty/pes_pipeline_mul/assets/84654826/79e91934-4653-4c0e-9020-661733b49a5a)


write the netlist 

```
write_verilog -noattr /home/adrika/vsd/sky130RTLDesignAndSynthesisWorkshop/assignment/pes_pipeline_mul_net.v
```


For the netlist generation use the following command :

```
iverilog /home/adrika/vsd/sky130RTLDesignAndSynthesisWorkshop/my_lib/verilog_model/primitives.v /home/adrika/vsd/sky130RTLDesignAndSynthesisWorkshop/my_lib/verilog_model/sky130_fd_sc_hd.v /home/adrika/vsd/sky130RTLDesignAndSynthesisWorkshop/assignment/pes_pipeline_mul_net.v /home/adrika/vsd/sky130RTLDesignAndSynthesisWorkshop/assignment/tb_pes_pipeline_mul.v
./a.out
gtkwave tb_pes_pipeline_mul.v
```

### Postsynthesis GLS :

![image](https://github.com/AdrikaMohanty/pes_pipeline_mul/assets/84654826/be9b5136-2d44-4cb5-98d7-a85f788c4cf6)


From this you can observe that the post-synthesis and pre synthesis simulation are same .

</details>

<details>
    <summary>
        POST-SYNTHESIS AND OPENLANE FLOW
    </summary>

### Synthesis :


Open the opnelane in interactive mode and run your desisgn 

```
./flow.tcl -interactive
package require openlane 0.9
prep -design pes_pipeline_mul
run_synthesis
```


![image](https://github.com/AdrikaMohanty/pes_pipeline_mul/assets/84654826/efd06c0c-0217-4743-8ab6-e903913b6a5a)

</details>
