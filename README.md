# google-cloud-speech-api-sample

Audio to Text

## Install sox

```bash
brew install sox --with-lame --with-flac --with-libvorbis
```

## Convert file from MP3 to RAW

```bash
sox k10010798551000.mp3 --channels=1 --bits=16 --rate=16000 --encoding=signed-integer --endian=little k10010798551000.raw
```

## Copy file to Google Cloud Storage

```bash
gsutil cp k10010798551000.raw gs://your-bucket-name
```

## Request Async Recognize

!!! You must set your project name in `async-reqeust.json` file

```bash
curl -s -H "Content-Type: application/json" \
    -H "Authorization: Bearer <access-token>" \
    https://speech.googleapis.com/v1beta1/speech:asyncrecognize \
    -d @async-request.json
```

save your name and fetch result later.

## Get Result

**Request**

```bash
curl -s -H "Authorization: Bearer <access-token>" https://speech.googleapis.com/v1beta1/operations/3261126959149734944
```

**Response**

```json
{
  "name": "3261126959149734944",
  "metadata": {
    "@type": "type.googleapis.com/google.cloud.speech.v1beta1.AsyncRecognizeMetadata",
    "progressPercent": 100,
    "startTime": "2016-12-11T08:48:27.517717Z",
    "lastUpdateTime": "2016-12-11T08:49:51.005093Z"
  },
  "done": true,
  "response": {
    "@type": "type.googleapis.com/google.cloud.speech.v1beta1.AsyncRecognizeResponse",
    "results": [
      {
        "alternatives": [
          {
            "transcript": "買い物のカードから子供が落ちる事故が多いスーパーやショッピングセンターには買い物中にしないものを入れるカートに子供が座る椅子がついているものがあります国民生活センターが三重病院に聞くと6歳以下の子供がカートから落ちたりする事故が今年10月までの約5年半の間に182ありましたこの中子供が頭や顔に怪我をした事故は91回ありました骨が折れたり頭を強く打ったりして入院した子供もいました",
            "confidence": 1
          }
        ]
      },
      {
        "alternatives": [
          {
            "transcript": "国民生活センターはスーパーなどは床がコンクリートと同じぐらい硬いため子供がカートから落ちると大きな怪我をする危険がありますしないものをいれるところに子供を座らせたり子供がカートの上で立ったりしないように気をつけてくださいと話しています",
            "confidence": 1
          }
        ]
      }
    ]
  }
}
```

## Links

- [Speech API - Speech Recognitio](https://cloud.google.com/speech/)
- [Language Support](https://cloud.google.com/speech/docs/languages)
- [APIs](https://cloud.google.com/speech/docs/apis)
- [Sample audio file - NEWS WEB EASY|買い物のカートから子どもが落ちる事故が多い](http://www3.nhk.or.jp/news/easy/k10010798551000/k10010798551000.html)
