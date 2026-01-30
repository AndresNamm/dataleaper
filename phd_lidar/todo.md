Here the focus is to get shit done. Move forward quickly

# Tmp

. Kuna üldine arusaam on olemas, siis tuleb jaotada tööd praktilise ja teoreetilise arusaama vahel

- Cloudcompare tee protsess läbi
- Saa aru matast, left hand coordinate system right hand system [Computing the Pixel Coordinates of a 3D Point](https://www.scratchapixel.com/lessons/3d-basic-rendering/computing-pixel-coordinates-of-3d-point/mathematics-computing-2d-coordinates-of-3d-points.html)

[Lidar e2e FingerPrint Process implementation Part I](https://www.notion.so/Lidar-e2e-FingerPrint-Process-implementation-Part-I-29d2e1a674b380b98c7ee325a61a9f94?pvs=21)

[Lidar e2e FingerPrint Process implementation Part II](lidar_fp_process_implementation_2.md)
[Experiment design](experiment_design.md)

# Todo

- [x]  Get Camera External Matrix from CloudCompare  [PROCESS TRYOUT ITERATION 1](https://www.notion.so/PROCESS-TRYOUT-ITERATION-1-2492e1a674b380708239e53a6f722418?pvs=21)
- [x]  Build the to projection workflow simply [Camera Transform](https://www.notion.so/Camera-Transform-2652e1a674b38030a94ae50b80e343af?pvs=21)
- [x]  Orhtographic projection sample buildout
- [x]  Implementeeri see protsess Open3D ja lidari peale Part I
- [ ]  Implementeeri see protsess Open3D ja lidari peale Part II
- [ ]  Experiment design
- [ ]  TLS method comparison Faro vs Iphone
- [ ]  Article method ready?
- [ ]  Iphone If not works — try method of calculating pixel distances based on
    - [ ]  Camera Intrinsics
    - [ ]  Depth
- [ ]  Article Ready

# Logi

## Jaanuar

- Sain tööle programmi, mis loeb sisse lidari faili, teeb ortograafilise projektsiooni 2D-sse säilitades pildi ja reaalse mõõtühikute vahelise süsteemi.
- Teostasin kontrollmõõtmise 2D pildi pealt

## August

- Sain esimest korda CloudCompare UI-ga ära testitud protsessi, kuidas Lidar globaalsed koordinaadid viia kaamera ( custom vaate) koordinaatsüsteemi. Natuke oli nuputamist, sest cloudcompare ei anna lihtsalt kaamerat maatriksit vaid ainult kaamerapunkti koordinaadi ning XYZ välised rotatsioonid kraadides, s.t mul tuli enne arvutada nendest kaamera maatriks ja siis oli juba punktidele transformatsiooni rakendamine lihtsam. [**https://github.com/AndresNamm/timber_detective/blob/main/ui/example_projection/test.ipynb**](https://github.com/AndresNamm/timber_detective/blob/main/ui/example_projection/test.ipynb)   .. Järgmiseks sammuks siis ortograafiline projektsioon ja ML mudeli jooksutamine 2D pildi peal. Sellest peaks saama siis lõppkokkuvõteks segmenteeritud punktipilve, mille pealt siis saab iga palkiotsa pindala arvutada.
- Martini Tagasiside
    - Vaatasin notebookile peale. võin kohe paar soovitust jagada, mis on elu palju kergemaks nende teemade juures teinud:
    1. asendi / pöörete esitamiseks ja rekandamiseks on väga mugav [**https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.transform.Rotation.html**](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.transform.Rotation.html)
    nt saad kohe teha r.as_euler('zyx', degrees=True)
    2. hea notatsioon muutujanimede juures on väga-väga suureks abiks koodi / matemaatika selguse jaoks ja vigade vältimiseks. peamine on kirjas siin [**https://rpg.ifi.uzh.ch/docs/teaching/2024/FurgaleTutorial.pdf**](https://rpg.ifi.uzh.ch/docs/teaching/2024/FurgaleTutorial.pdf)
    aga ise tööl kasutan seda notatsiooni:
    // Notation
    // local_X_body - position of body in local frame, equivalent to local_X_local2body
    // local_X_body2sensor - translation from body to sensor expressed in local frame coordinates
    //                local_X_body + local_X_body2sensor = local_X_sensor
    // local_R_body - orientation of body relative to local frame / active rotation from body to local
    //                local_R_body * body_R_sensor = local_R_sensor
    //                local_R_body * body_X_sensor = local_X_body2sensor
    // local_T_body - pose of body in local frame / active transform of body frame points to local frame
    //                local_T_body * body_T_sensor = local_T_sensor
    //                local_T_body * body_X_sensor = local_X_sensor
    // local_vel_sensor - velocity of sensor object expressed in local frame coordinates
    //                local_R_body * body_ang_vel_body = local_ang_vel_body
    
    [**docs.scipy.org**](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.transform.Rotation.html)
    
    - ja punktipilvedega toimetamiseks ning kuvamiseks Pythonis on Open3D päris hea
- Augusti Tegevuste ja [Taskide Logi](https://www.notion.so/PROCESS-TRYOUT-ITERATION-1-2492e1a674b380708239e53a6f722418?pvs=21)

# Goal

Ehitan rakendust, mis võimaldab läbi teha protsessi

1. Lidarist Snapshot RGB mudeli maailma
2. RGB Snapshotist Segmenteerimine
3. 2D peal stock coeficcient, areas ….
4. Tagasi punktipilve maailma 
5. .. Pinnanormaalidega toimetamine, et segmentatsiooni veelgi parandada

Järgin põhimõtet, et päev researchin ja päev mõtlen, kui keerulisem teema on. Lihtsamaga pole vaja. Vahel vaja vahel rohkem mõtlemist — punkti olulisus on see, et ma lihtsalt raske teemaga ei keskendu ainult uue info saamisele vaid info läbi mõtlemisele.

# References

1. [2D->3D - Miro](https://miro.com/app/board/uXjVIhHiYMc=/)
2. [Display modes - CloudCompareWiki](https://www.cloudcompare.org/doc/wiki/index.php/Display_modes)
3. [The Difference Between Perspective and Orthographic - Blender 3.0 Tutorial](https://www.youtube.com/watch?v=dUJzpz8J9xw&ab_channel=TutsByKai)
4. [Perspektiiv VS Ortograafiline - Miro](https://miro.com/app/board/uXjVIhflz5g=/)
5. [projection-1.pdf](https://aditipaulsite.wordpress.com/wp-content/uploads/2019/02/projection-1.pdf) Päris hea võrdluse perspective vs orthogonal. Kokkuvõte teemast.
6. https://m.youtube.com/watch?v=NaclfcHReXk&pp=ygUcb3J0aG9ncmFwaGljIHByb2plY3Rpb24gbWF0aA%3D%3D - ülihea seletus teemasse
7. https://learngeodata.eu/visualise-massive-point-cloud-in-python/

[3D-2D-3D process math](https://www.notion.so/3D-2D-3D-process-math-2282e1a674b38087b12ff5e21e72d2c1?pvs=21) 

[TODO archive](https://www.notion.so/TODO-archive-2652e1a674b3802ab306f62f6e5864cb?pvs=21)

[PROCESS TRYOUT ITERATION 1](https://www.notion.so/PROCESS-TRYOUT-ITERATION-1-2492e1a674b380708239e53a6f722418?pvs=21)

[Peast välja kirjutatud Protsess](https://www.notion.so/Peast-v-lja-kirjutatud-Protsess-22b2e1a674b38063a193d1c50e922d6e?pvs=21)

[Getting Camera Matrix Coordinates from cloudcomapre](https://www.notion.so/Understanding-Camera-Coordinate-Transformations-2442e1a674b3809386c3ea125e65a9d7?pvs=21) 

[Orthographic Projection](https://www.notion.so/Orthographic-Projection-2442e1a674b3809d8f2fd95d55a1b3b8?pvs=21) — MATH

[Camera Transform](https://www.notion.so/Camera-Transform-2652e1a674b38030a94ae50b80e343af?pvs=21)