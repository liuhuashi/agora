# 声网生成token

---

## 例子

```php
use DateTime;
use DateTimeZone;
use Agora\RtcTokenBuilder;
use Agora\RtmTokenBuilder;

/**
 * 语音通话token
 *
 * @param RtcTokenRequest $request
 * @return array
 * @throws \Exception
 */
public function rtcToken(RtcTokenRequest $request)
{
    $appID = config('agora.app_id');
    $appID = '970CA35de60c44645bbae8a215061b33';
    $appCertificate = config('agora.app_certificate');
    $appCertificate = '5CFd2fd1755d40ecb72977518be15d3b';

    $channelName = request('channel_name');
    $uidStr = request('uid');

    $role = RtcTokenBuilder::RoleAttendee;
    $expireTimeInSeconds = 3600;
    $currentTimestamp = (new DateTime("now", new DateTimeZone('UTC')))->getTimestamp();
    $privilegeExpiredTs = $currentTimestamp + $expireTimeInSeconds;

    $token = RtcTokenBuilder::buildTokenWithUserAccount($appID, $appCertificate, $channelName, $uidStr, $role, $privilegeExpiredTs);

    return $this->display($token);
}

/**
 * 实时消息token
 *
 * @param RtmTokenRequest $request
 * @return array
 * @throws \Exception
 */
public function rtmToken(RtmTokenRequest $request)
{
    $appID = config('agora.app_id');
    $appID = '970CA35de60c44645bbae8a215061b33';
    $appCertificate = config('agora.app_certificate');
    $appCertificate = '5CFd2fd1755d40ecb72977518be15d3b';

    $uidStr = request('uid');

    $role = RtmTokenBuilder::RoleRtmUser;
    $expireTimeInSeconds = 3600;
    $currentTimestamp = (new DateTime("now", new DateTimeZone('UTC')))->getTimestamp();
    $privilegeExpiredTs = $currentTimestamp + $expireTimeInSeconds;

    $token = RtmTokenBuilder::buildToken($appID, $appCertificate, $uidStr, $role, $privilegeExpiredTs);

    return $this->display($token);
}
```

