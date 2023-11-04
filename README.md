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


## Floorplanning 

```
run_floorplan
```

after this to view floor plan run the following commands 

```
cd /home/adrika/OpenLane/designs/pes_pipeline_mul/runs/RUN_2023.11.04_08.30.59/results/floorplan

magic -T /home/adrika/sky130 lef read /home/adrika/OpenLane/designs/pes_pipeline_mul/runs/RUN_2023.11.04_08.30.59/tmp/merged.nom.lef def read pes_pipeline_mul.def &
```




![image](https://github.com/AdrikaMohanty/pes_pipeline_mul/assets/84654826/75871203-a0d6-4827-8a6d-cd14d4011a71)

## Placement 

```
run_placement
```

![image](https://github.com/AdrikaMohanty/pes_pipeline_mul/assets/84654826/561f359a-dabc-4f41-b38b-414df5c2086f)


![image](https://github.com/AdrikaMohanty/pes_pipeline_mul/assets/84654826/4f187b53-c694-47df-81f1-8f63d8f6b64f)


## Clock tree synthesis 

After placement we do the clock tree synthesis
```
run_cts
```

![image](https://github.com/AdrikaMohanty/pes_pipeline_mul/assets/84654826/93184502-4e80-4292-b2e9-74b14cab5500)


## PDN 

After clock tree synthesis generate the pdn
```
gen_pdn
```

## Routing 

The final step now is routing 

If you dont get the output there is a chance that the area you decided in config file might be too small , in such situation please reconsider changing it 




### For automated flow 

```
cd OpenLane
sudo make mount
./flow.tcl -design <design name>
```



</details>
