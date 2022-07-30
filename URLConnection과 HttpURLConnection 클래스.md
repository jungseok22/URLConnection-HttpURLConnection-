# <URLConnection과 HttpURLConnection 클래스>



## 1. URL 객체 생성

- 다음과 같이 주어진 URL 주소에 대해 새 URL 객체를 생성한다

  ->  URL url = new URL("http://www.google.com");

  이 생성자는 URL 형식이 잘못된 경우 MalformedURLException을 throw한다. 이 예외는 IOException의 하위 클래스다.

## 2. URL에서 URLConnection 객체 얻기

- URLConnection 인스턴스는 URL 객체의 openConnection() 메소드 호출에 의하여 얻어진다

  -> URLConnection urlCon = url.openConnection();

- 프로토콜이 http://인 경우 반환된 객체를 HttpURLConnection 객체로 캐스팅할 수 있다.

  -> HttpURLConnection httpCon = (HttpURLConnection) url.openConnection();

  

## 3. URLConnection 구성

- 실제로 연결을 설정하기 전에 타임아웃 ,캐시,HTTP 요청 방법 등과 같이 클라이언트와 서버 간의 다양한 옵션을 설정할 수 있다.

  - **setConnectTimeout** (int timeout) : 연결 타임아웃 값을 설정한다(단위 : 밀리초).

  - **setReadTimeout** (int timeout) : 읽기 타임아웃 값을 설정한다(단위 : 밀리초). 제한 시간이 만료되고 연결의 입력 스트림에서 읽을 수 있는 데이터가 없으면 SocketTimeoutException이 발생한다. 시간 초과가 0이면, 무한대 타임아웃(기본값)을 의미한다.

  - **setDefaultUseCaches** (boolean default) : URLConnection이 기본적으로 캐시를 사용하는지 여부를 설정한다(기본값은 true). 이 메서드는 URLConnection 클래스의 다음 인스턴스에 영향을 준다.

  - **setUseCaches** (boolean useCaches) : 연결이 캐시를 사용하는지 여부를 설정한다(기본값은 true).

  - **setDoInput** (boolean doInput) : URLConnection을 서버에서 콘텐츠를 읽는 데 사용할 수있는지 여부를 설정한다(기본값은 true).

  - **setDoOutput** (boolean doOutput) : URLConnection이 서버에 데이터를 보내는 데 사용할 수있는지 여부를 설정한다(기본값은 false).

  - **setAllowUserInteraction** (boolean allow) : 사용자 상호 작용을 활성화 또는 비활성화한다. 예를 들어 필요한 경우 인증 대화 상자를 표시한다(기본값은 false).

  - **setDefaultAllowUserInteraction** (boolean default) : 이후의 모든 URLConnection객체에 대한 사용자 상호 작용의 기본값을 설정한다.

  - **setRequestMethod** (String  method) : HTTP 메소드 GET, POST, HEAD, OPTIONS, PUT, DELETE, TRACE 중 하나인 URL 요청에 대한 메소드를 설정합니다. 기본값은 GET이다.

  - **setChunkedStreamingMode** (int chunkLength) : 콘텐츠 길이를 미리 알 수 없는 경우 내부 버퍼링 없이 HTTP 요청 본문을 스트리밍할 수 있다.

  - **setFixedLengthStreamingMode** (long contentLength) : 콘텐츠 길이를 미리 알고 있는 경우 내부 버퍼링 없이 HTTP 요청 본문을 스트리밍할 수 있다.

  - **setFollowRedirects** (boolean follow) : 이 정적 메서드는 HTTP 리다이렉션 뒤에 이 클래스의 미래 개체가 자동으로 따라야 하는지 여부를 설정한다(기본값은 true).

    

## 4. 헤더 필드 읽기

- 연결이 이루어지면 서버는 URL 요청을 처리하고 메타데이터와 실제 콘텐츠로 구성된 응답을 다시 보낸다. 메타데이터는 헤더 필드라고 하는 키=값 쌍의 모음이다. 헤더 필드는 서버에 대한 정보, 상태 코드, 프로토콜 정보 등을 나타낸다. 실제 내용은 문서의 유형에 따라 텍스트, HTML, 이미지 등이 될 수 있다. URLConnection 클래스는 헤더 필드를 읽기 위한 다음과 같은 방법을 제공한다
  - **getHeaderFields** () : 모든 헤더 필드를 포함하는 맵을 반환한다. 키는 필드 이름이고 값은 해당 필드 값을 나타내는 문자열 목록이다.
  - **getHeaderField** (int n) : n 번째 헤더 필드의 값을 읽는다.
  - **getHeaderField** (String name) : 명명된 헤더 필드의 값을 읽는다.
  - **getHeaderFieldKey** (int n) : n 번째 헤더 필드의 키를 읽는다.
  - **getHeaderFieldDate** (String name, long default) : Date로 구문 분석된 명명된 필드의 값을 읽는다. 필드가 없거나 값 형식이 잘못된 경우 기본값이 대신 반환된다.
  - **getHeaderFieldInt** (String name, int default) : 정수로 구문 분석된 명명된 필드의 값을 읽는다. 필드가 없거나 값 형식이 잘못된 경우 기본값이 대신 반환된다.
  - **getContentEncoding** () : 콘텐츠의 인코딩 유형을 나타내는 콘텐츠 인코딩 헤더 필드의 값을 읽는다.
  - **getContentLength** () : 콘텐츠의 크기(바이트)를 나타내는 콘텐츠 길이 헤더 필드의 값을 읽는다.
  - **getContentType** () : 컨텐츠의 유형을 나타내는 컨텐츠 유형 헤더 필드의 값을 읽는다.
  - **getDate** () : 서버의 날짜 시간을 나타내는 날짜 헤더 필드의 값을 읽는다.
  - **getExpiration** () : 만료 헤더 필드의 값을 읽고 응답이 오래된 것으로 간주되는 시간을 나타낸다. 이는 캐시 제어를 위한 것이다.
  - **getLastModified** () : 컨텐츠의 마지막 수정 시간을 나타내는 last-modified 헤더 필드의 값을 읽는다. 그리고 서브클래스 HttpURLConnection 은 추가 메소드를 제공한다: