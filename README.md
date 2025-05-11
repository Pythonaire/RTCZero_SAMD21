The SAMD21 mcu has a internal 48 kHz and a external 32kHz oscillator. It seems to me the internal 48 kHz oscillator is not stable. This is a modified Arduino driver to address the external 32 kHz oscillator. Using that, for me, the driver works stable. It can be used in the same way, as the Arduino driver:

#include <RTCZero.h>

...
rtc.begin(resetTime);
  rtc.setTime(hours, minutes, seconds);
  rtc.setDate(day, month, year);

...
rtc.setAlarmMinutes(wait);
rtc.setAlarmSeconds(0);
rtc.enableAlarm(rtc.MATCH_MMSS);
rtc.attachInterrupt(alarmMatch);
rtc.standbyMode();
};
void alarmMatch() {
  rtc.setTime(hours, minutes, seconds);
  rtc.setDate(day, month, year);
};
