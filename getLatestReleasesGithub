<?php

$Data = getLatestReleasesGithub('2dust', 'v2rayng');
function getLatestReleasesGithub($author, $repository)
{
    $Releases = json_decode(getURL('https://api.github.com/repos/' . $author . '/' . $repository . '/releases'), true);
    $Data['latest'] = $Data['prerelease'] = NULL;
    for ($i = 0; $i < count($Releases); $i++) {
        if (!isset($Data['prerelease']['tag']) && $Releases[$i]['prerelease']) {
            $Data['prerelease']['tag'] = $Releases[$i]['tag_name'];
            for ($l = 0, $n = 0; $l < count($Releases[$i]['assets']); $l++) {
                $Data['prerelease']['links'][$n]['name'] = explode('.', $Releases[$i]['assets'][$l]['name']);
                array_pop($Data['prerelease']['links'][$n]['name']);
                $Data['prerelease']['links'][$n]['name'] = implode('.', $Data['prerelease']['links'][$n]['name']);
                $Data['prerelease']['links'][$n]['name'] = substr($Data['prerelease']['links'][$n]['name'], strpos($Data['prerelease']['links'][$n]['name'], $Data['prerelease']['tag']) + strlen($Data['prerelease']['tag']) + 1);
                switch ($Data['prerelease']['links'][$n]['name']) {
                    case 'armeabi-v7a':
                        $Data['prerelease']['links'][$n]['name'] = 'ARMv7-A';
                        break;
                    case 'arm64-v8a':
                        $Data['prerelease']['links'][$n]['name'] = 'ARMv8-A';
                        break;
                    case '':
                        $Data['prerelease']['links'][$n]['name'] = 'All-Android';
                        break;
                }
                $Data['prerelease']['links'][$n]['size'] = $Releases[$i]['assets'][$l]['size'];
                $Data['prerelease']['links'][$n]['url'] = $Releases[$i]['assets'][$l]['browser_download_url'];
                $n++;
            }
        }
        if (!isset($Data['latest']['tag']) && !$Releases[$i]['prerelease']) {
            $Data['latest']['tag'] = $Releases[$i]['tag_name'];
            for ($l = 0, $n = 0; $l < count($Releases[$i]['assets']); $l++) {
                $Data['latest']['links'][$n]['name'] = explode('.', $Releases[$i]['assets'][$l]['name']);
                array_pop($Data['latest']['links'][$n]['name']);
                $Data['latest']['links'][$n]['name'] = implode('.', $Data['latest']['links'][$n]['name']);
                $Data['latest']['links'][$n]['name'] = substr($Data['latest']['links'][$n]['name'], strpos($Data['latest']['links'][$n]['name'], $Data['latest']['tag']) + strlen($Data['latest']['tag']) + 1);
                switch ($Data['latest']['links'][$n]['name']) {
                    case 'armeabi-v7a':
                        $Data['latest']['links'][$n]['name'] = 'ARMv7-A';
                        break;
                    case 'arm64-v8a':
                        $Data['latest']['links'][$n]['name'] = 'ARMv8-A';
                        break;
                    case '':
                        $Data['latest']['links'][$n]['name'] = 'All-Android';
                        break;
                }
                $Data['latest']['links'][$n]['size'] = $Releases[$i]['assets'][$l]['size'];
                $Data['latest']['links'][$n]['url'] = $Releases[$i]['assets'][$l]['browser_download_url'];
                $n++;
            }
        }
    }
    return $Data;
}
function getURL($URL)
{
    $curl = curl_init();
    curl_setopt_array($curl, array(
        CURLOPT_URL => $URL,
        CURLOPT_RETURNTRANSFER => true,
        CURLOPT_ENCODING => '',
        CURLOPT_MAXREDIRS => 10,
        CURLOPT_TIMEOUT => 0,
        CURLOPT_FOLLOWLOCATION => true,
        CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
        CURLOPT_CUSTOMREQUEST => 'GET',
    ));

    $response = curl_exec($curl);
    curl_close($curl);
    return $response;
}
