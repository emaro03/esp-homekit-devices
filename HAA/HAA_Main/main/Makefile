PROGRAM = haamain

SETUP_WEB := $(shell python3 ../../common/embed.py setup.html > setup.html.h)

EXTRA_COMPONENTS = \
	extras/dhcpserver \
	extras/rboot-ota \
	$(abspath ../../../external_libs/http-parser) \
    $(abspath ../../../external_libs/wolfssl) \
    $(abspath ../../../libs/cJSON-rsf) \
    $(abspath ../../../libs/homekit-rsf) \
	$(abspath ../../../libs/adv_i2c) \
    $(abspath ../../../libs/adv_button) \
    $(abspath ../../../libs/adv_hlw) \
	$(abspath ../../../libs/adv_pwm) \
	$(abspath ../../../libs/adv_nrzled) \
	$(abspath ../../../libs/new_dht) \
	$(abspath ../../../libs/new_onewire) \
	$(abspath ../../../libs/new_ds18b20) \
	$(abspath ../../../libs/raven_ntp) \
	$(abspath ../../../libs/rs_ping) \
	$(abspath ../../../libs/unistring) \
	$(abspath ../../../libs/form_urlencoded) \
	$(abspath ../../../libs/adv_logger_ntp) \
	$(abspath ../../../libs/timers_helper)

FLASH_SIZE = 1
FLASH_MODE = dout
FLASH_SPEED = 40

# Max HAA firmware size is 585728 bytes

#EXTRA_CFLAGS += -O2 \
#	-fpredictive-commoning \
#	-ftree-slp-vectorize \
#	-fgcse-after-reload \
#	-floop-interchange \
#	-fvect-cost-model \
#	-ftree-partial-pre \
#	-ftree-loop-distribution \
#	-fipa-cp-clone \
#	-funswitch-loops \
#	-fpeel-loops \

EXTRA_CFLAGS += -Wall -std=gnu99
EXTRA_CFLAGS += -Wextra -Wno-unused-parameter
#EXTRA_CFLAGS += -Wpedantic

EXTRA_CFLAGS += -DHOMEKIT_SHORT_APPLE_UUIDS
EXTRA_CFLAGS += -DSPIFLASH_HOMEKIT_BASE_ADDR=0xF2000
EXTRA_CFLAGS += -DHOMEKIT_OVERCLOCK_PAIR_VERIFY
EXTRA_CFLAGS += -DHOMEKIT_OVERCLOCK_PAIR_SETUP
EXTRA_CFLAGS += -DHOMEKIT_DISABLE_MAXLEN_CHECK
EXTRA_CFLAGS += -DHOMEKIT_DISABLE_VALUE_RANGES
#EXTRA_CFLAGS += -DHOMEKIT_NOTIFY_EVENT_ENABLE
#EXTRA_CFLAGS += -DHOMEKIT_SERVER_ON_RESOURCE_ENABLE
#EXTRA_CFLAGS += -DHOMEKIT_CHANGE_MAX_CLIENTS

EXTRA_CFLAGS += -DHAA_CHIP_NAME=\"esp8266\"

EXTRA_CFLAGS += -DTCP_MSS=1460
EXTRA_CFLAGS += -DTCP_WND=5840
EXTRA_CFLAGS += -DTCP_SND_BUF=5840
EXTRA_CFLAGS += -DLWIP_WND_SCALE=1 -DTCP_RCV_SCALE=0

EXTRA_CFLAGS += -DLWIP_NETIF_HOSTNAME=1
EXTRA_CFLAGS += -DLWIP_RAW=1
EXTRA_CFLAGS += -DARP_TABLE_SIZE=10
EXTRA_CFLAGS += -DDNS_MAX_RETRIES=2
EXTRA_CFLAGS += -DDHCP_DOES_ARP_CHECK=0
EXTRA_CFLAGS += -DLWIP_DHCP_AGGRESSIVE
EXTRA_CFLAGS += -DLWIP_DHCP_RANDOMIZE_COARSE_TIME_SECS=10
EXTRA_CFLAGS += -DDEFAULT_RAW_RECVMBOX_SIZE=5
EXTRA_CFLAGS += -DMEMP_NUM_NETCONN=16
#EXTRA_CFLAGS += -DCHECKSUM_CHECK_UDP=0
#EXTRA_CFLAGS += -DMEMP_NUM_RAW_PCB=1
#EXTRA_CFLAGS += -DMEMP_NUM_UDP_PCB=3
#EXTRA_CFLAGS += -DMEMP_NUM_TCP_PCB=9
#EXTRA_CFLAGS += -DMEMP_NUM_TCP_PCB_LISTEN=1

EXTRA_CFLAGS += -DDHCP_SERVER_MAX_LEASES=2

EXTRA_CFLAGS += -DWIFI_PARAM_SAVE=0

EXTRA_CFLAGS += -DconfigMAX_TASK_NAME_LEN=7
EXTRA_CFLAGS += -DconfigCHECK_FOR_STACK_OVERFLOW=2
EXTRA_CFLAGS += -DconfigMINIMAL_STACK_SIZE=256
EXTRA_CFLAGS += -DconfigTIMER_TASK_PRIORITY=\(configMAX_PRIORITIES-3\)
EXTRA_CFLAGS += -DconfigTIMER_QUEUE_LENGTH=15
EXTRA_CFLAGS += -DconfigTIMER_TASK_STACK_DEPTH=736

## HAA DEBUG
#EXTRA_CFLAGS += -DHAA_DEBUG

## FREERTOS DEBUG
#EXTRA_CFLAGS += -DconfigUSE_TRACE_FACILITY

## LWIP DEBUG
#EXTRA_CFLAGS += -DLWIP_DEBUG

## LWIP STATS
#EXTRA_CFLAGS += -DLWIP_STATS=1 -DLWIP_STATS_DISPLAY=1 -DMEMP_STATS=1

## HAA POWER MONITOR DEBUG
#EXTRA_CFLAGS += -DPOWER_MONITOR_DEBUG

## HAA LIGHTBULB DEBUG
#EXTRA_CFLAGS += -DLIGHT_DEBUG

## HOMEKIT DEBUG
#EXTRA_CFLAGS += -DHOMEKIT_DEBUG

## mDNS Responder DEBUG
#EXTRA_CFLAGS += -DqDebugLog -DqLogIncoming -DqLogAllTraffic

include $(abspath ../../../sdk/esp-open-rtos-rsf/common.mk)

LIBS += m

sign:
	../../common/ota_sign.sh
	
monitor:
	$(FILTEROUTPUT) --port $(ESPPORT) --baud 115200 --elf $(PROGRAM_OUT)
