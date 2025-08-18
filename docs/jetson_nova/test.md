# nova_preflight_checker

!!!warning
    Jetson Orin Nova Developer Kitでは時刻同期に時間がかかります。 `date`コマンドで、時刻が現在時刻になっていることを確認してから、checkerを起動します。

!!!warning
    Jetson Orin Nova Developer KitのUSB電源が本体電源ですが、カメラの電源はDC電源になります。2つの電源が接続されていないとエラーになります。

## nova_preflight_checker

```
nova_preflight_checker
```

```
======================================= test session starts ========================================
platform linux -- Python 3.10.12, pytest-8.3.4, pluggy-1.5.0 -- /opt/nvidia/nova/python/venv/bin/python3
cachedir: .pytest_cache
rootdir: /opt/nvidia/nova
configfile: pytest.ini
plugins: timeout-2.3.1
timeout: 30.0s
timeout method: signal
timeout func_only: False
collected 77 items                                                                                 

compute/pfc/tests.py::test_service[nova-tegra-stats@1000] PASSED                             [  1%]
compute/pfc/tests.py::test_service[nova-over-current-monitor@1] PASSED                       [  2%]
compute/pfc/tests.py::test_service[nova-power-monitor@1] PASSED                              [  3%]
compute/pfc/tests.py::test_service[nova-nvpower] PASSED                                      [  5%]
compute/pfc/tests.py::test_service[nova-jetson-clocks] PASSED                                [  6%]
compute/pfc/tests.py::test_nvme_parameters PASSED                                            [  7%]
compute/pfc/tests.py::test_service_irqbalance PASSED                                         [  9%]
logrotate/pfc/tests.py::test_service[logrotate] PASSED                                       [ 10%]
ptp/pfc/tests.py::test_service[nova-ptp4l@eno1] PASSED                                       [ 11%]
ptp/pfc/tests.py::test_service[nova-ptp-pre] PASSED                                          [ 12%]
ptp/pfc/tests.py::test_device PASSED                                                         [ 14%]
nvpps/pfc/tests.py::test_service[nova-mgbe0-latch] PASSED                                    [ 15%]
nvpps/pfc/tests.py::test_nvpps_device PASSED                                                 [ 16%]
nvpps/pfc/tests.py::test_nvpps_ioctl_timestamp PASSED                                        [ 18%]
nvpps/pfc/tests.py::test_nvpps_ioctl_event PASSED                                            [ 19%]
time/pfc/tests.py::test_service[nova-sync-time] PASSED                                       [ 20%]
time/pfc/tests.py::test_service[nova-phc2sys@eno1] PASSED                                    [ 22%]
time/pfc/tests.py::test_service[ntp] PASSED                                                  [ 23%]
time/pfc/tests.py::test_latch PASSED                                                         [ 24%]
time/pfc/tests.py::test_phc2sys_offsets PASSED                                               [ 25%]
time/pfc/tests.py::test_phc2sys_frequency PASSED                                             [ 27%]
time/pfc/tests.py::test_rtc0_device PASSED                                                   [ 28%]
metadata/pfc/tests.py::test_service[nova-metadata-generator] PASSED                          [ 29%]
wallpaper/pfc/tests.py::test_wallpaper_set PASSED                                            [ 31%]
jtop/pfc/tests.py::test_service[jtop] PASSED                                                 [ 32%]
dtb/pfc/tests.py::test_hawk_owl_p3762_dtb_overlay PASSED                                     [ 33%]
argus/pfc/tests.py::test_service[nova-gpio-fix] PASSED                                       [ 35%]
argus/pfc/tests.py::test_service[nova-argus-restart] PASSED                                  [ 36%]
hawk/pfc/tests.py::test_service[nvargus-daemon] PASSED                                       [ 37%]
hawk/pfc/tests.py::TestHawkEeprom::test_serial_number[front_stereo_camera] PASSED            [ 38%]
hawk/pfc/tests.py::TestHawkEeprom::test_img_size[front_stereo_camera-left_cam_intr] PASSED   [ 40%]
hawk/pfc/tests.py::TestHawkEeprom::test_img_size[front_stereo_camera-right_cam_intr] PASSED  [ 41%]
hawk/pfc/tests.py::TestHawkEeprom::test_gravity_acceleration[front_stereo_camera] PASSED     [ 42%]
hawk/pfc/tests.py::TestHawkEeprom::test_finite[front_stereo_camera] PASSED                   [ 44%]
hawk/pfc/tests.py::TestHawkEeprom::test_non_zero[front_stereo_camera-nm/update_rate] PASSED  [ 45%]
hawk/pfc/tests.py::TestHawkEeprom::test_non_zero[front_stereo_camera-nm/linear_acceleration_noise_density] PASSED [ 46%]
hawk/pfc/tests.py::TestHawkEeprom::test_non_zero[front_stereo_camera-nm/linear_acceleration_random_walk] PASSED [ 48%]
hawk/pfc/tests.py::TestHawkEeprom::test_non_zero[front_stereo_camera-nm/angular_velocity_noise_density] PASSED [ 49%]
hawk/pfc/tests.py::TestHawkEeprom::test_non_zero[front_stereo_camera-nm/angular_velocity_random_walk] PASSED [ 50%]
hawk/pfc/tests.py::TestHawkEeprom::test_serial_number[right_stereo_camera] PASSED            [ 51%]
hawk/pfc/tests.py::TestHawkEeprom::test_img_size[right_stereo_camera-left_cam_intr] PASSED   [ 53%]
hawk/pfc/tests.py::TestHawkEeprom::test_img_size[right_stereo_camera-right_cam_intr] PASSED  [ 54%]
hawk/pfc/tests.py::TestHawkEeprom::test_gravity_acceleration[right_stereo_camera] PASSED     [ 55%]
hawk/pfc/tests.py::TestHawkEeprom::test_finite[right_stereo_camera] PASSED                   [ 57%]
hawk/pfc/tests.py::TestHawkEeprom::test_non_zero[right_stereo_camera-nm/update_rate] PASSED  [ 58%]
hawk/pfc/tests.py::TestHawkEeprom::test_non_zero[right_stereo_camera-nm/linear_acceleration_noise_density] PASSED [ 59%]
hawk/pfc/tests.py::TestHawkEeprom::test_non_zero[right_stereo_camera-nm/linear_acceleration_random_walk] PASSED [ 61%]
hawk/pfc/tests.py::TestHawkEeprom::test_non_zero[right_stereo_camera-nm/angular_velocity_noise_density] PASSED [ 62%]
hawk/pfc/tests.py::TestHawkEeprom::test_non_zero[right_stereo_camera-nm/angular_velocity_random_walk] PASSED [ 63%]
hawk/pfc/tests.py::TestHawkEeprom::test_serial_number[left_stereo_camera] PASSED             [ 64%]
hawk/pfc/tests.py::TestHawkEeprom::test_img_size[left_stereo_camera-left_cam_intr] PASSED    [ 66%]
hawk/pfc/tests.py::TestHawkEeprom::test_img_size[left_stereo_camera-right_cam_intr] PASSED   [ 67%]
hawk/pfc/tests.py::TestHawkEeprom::test_gravity_acceleration[left_stereo_camera] PASSED      [ 68%]
hawk/pfc/tests.py::TestHawkEeprom::test_finite[left_stereo_camera] PASSED                    [ 70%]
hawk/pfc/tests.py::TestHawkEeprom::test_non_zero[left_stereo_camera-nm/update_rate] PASSED   [ 71%]
hawk/pfc/tests.py::TestHawkEeprom::test_non_zero[left_stereo_camera-nm/linear_acceleration_noise_density] PASSED [ 72%]
hawk/pfc/tests.py::TestHawkEeprom::test_non_zero[left_stereo_camera-nm/linear_acceleration_random_walk] PASSED [ 74%]
hawk/pfc/tests.py::TestHawkEeprom::test_non_zero[left_stereo_camera-nm/angular_velocity_noise_density] PASSED [ 75%]
hawk/pfc/tests.py::TestHawkEeprom::test_non_zero[left_stereo_camera-nm/angular_velocity_random_walk] PASSED [ 76%]
hawk/pfc/tests.py::test_hawk_capture[front_stereo_camera] PASSED                             [ 77%]
hawk/pfc/tests.py::test_hawk_capture[right_stereo_camera] PASSED                             [ 79%]
hawk/pfc/tests.py::test_hawk_capture[left_stereo_camera] PASSED                              [ 80%]
hawk/pfc/tests.py::test_hawk_i2c_rate PASSED                                                 [ 81%]
hawk/pfc/tests.py::test_total_hawk_devices PASSED                                            [ 83%]
owl/pfc/tests.py::test_total_owl_devices PASSED                                              [ 84%]
owl/pfc/tests.py::test_owl_capture[front_fisheye_camera] PASSED                              [ 85%]
owl/pfc/tests.py::test_owl_capture[right_fisheye_camera] PASSED                              [ 87%]
owl/pfc/tests.py::test_owl_capture[left_fisheye_camera] PASSED                               [ 88%]
bmi088/pfc/tests.py::TestBmi088Imu::test_nominal_freq[front_stereo_imu] PASSED               [ 89%]
bmi088/pfc/tests.py::TestBmi088Imu::test_simultanous_freq[front_stereo_imu] PASSED           [ 90%]
bmi088/pfc/tests.py::TestBmi088Imu::test_nominal_freq[chassis_imu] PASSED                    [ 92%]
bmi088/pfc/tests.py::TestBmi088Imu::test_simultanous_freq[chassis_imu] PASSED                [ 93%]
bmi088/pfc/tests.py::test_total_bmi088_devices PASSED                                        [ 94%]
ssd/pfc/tests.py::test_ssd_write_speed PASSED                                                [ 96%]
ssd/pfc/tests.py::test_filesystem_ssd PASSED                                                 [ 97%]
ssd/pfc/tests.py::test_recordings_permissions PASSED                                         [ 98%]
calibration/pfc/tests.py::test_calibration_host PASSED                                       [100%]

======================================= 77 passed in 40.86s ========================================
```

