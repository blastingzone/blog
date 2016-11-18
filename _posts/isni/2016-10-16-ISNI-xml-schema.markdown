---
layout: post
title:  "ISNI Request XML 스키마"
date:   2016-10-16 16:20:00 +0900
categories: ISNI
tags: isni
---
### ISNI

ISNI란 <b>I</b>nternational <b>S</b>tandard <b>N</b>ame <b>I</b>dentifier의 약자다.
책, TV 프로그램, 신문 기사, 음악, 미술 등 미디어 컨텐츠에 기여한 사람들을 유니크하게 식별할 수 있는 부호이다.

### Request XML Schema

{% highlight xml %}
  <Request>
    <requestID>
      <dateTimeOfRequest>
        YYYY-MM-DD HH:MM:SS
      </dateTimeOfRequest>
      <requestorTransactionID>
        요청자가 생성한 문자열
      </requestorTransactionID>
    </requestID>
    <identityInformation>
      <requestorIdentifierOfIdentity>
        <referenceURI>
          이 항목은 Deprecated 되었음. 추후 삭제될 것이다.
        </referenceURI>
        <Identifier>
          식별자
        </Identifier>
        <deprecatedLocalIdentifier>
          identifier를 합쳐야 하는 경우 등에 사용하는 옵션.
          참고로 공식 Doc에 '반복 불가' 필드로 되어 있는데 표기 오류로 의심된다.
          이 필드의 속성은 반복 가능해야 말이 된다.
        </deprecatedLocalIdentifier>
        <specialStatus>
          validation이 필요없는 정보. 예를 들어 국가 납본 관련 정보 등.
        </specialStatus>
      </requestorIdentifierOfIdentity>
      <otherIdentifierOfIdentity>
        <identifier>
        </identifier>
        <type>
          identifier의 이름. 메타 정보 변경이나 merge 요청 등에 사용한다.
        </type>
      </otherIdentifierOfIdentity>
      <identity>
        /* identity는 크게 2가지 경우가 있는데,
          personOrFiction이나 organisation의 경우 내용이 달라진다. */
        <personOrFiction>
          <personalName>
            <nameUse>
              다음 중 하나 : public, public and private, private, fictional character, unknown
            </nameUse>
            <surname>
              이름이 2개 이상이거나 여러 부분으로 되어 있을 때 주로 사용되는 호칭
              추가정보는 personalNameVariant에 작성할 것
            </surname>
            <forename>
              성을 제외한 모든 이름(forename)또는 대문자를 포함해야 함
            </forename>
            <numeration>
               III, 3rd 등의 숫자 표기
            </numeration>
            <nameTitle>
              Sir, Hon 등의 타이틀
            </nameTitle>
            <marcDate>
              출생일 / 사망일을 ISO 8601 규칙에 맞춰서 제공할 수 없을 경우.
              이 항목에 쓰인 값은 public interfaces에 나타난다.
            </marcDate>
            <languageOfName>
              ISO 639-2 2 character code http://id.loc.gov/vocabulary/iso639-2
            </languageOfName>
            <script>
              ISO 15924 4 letter code www.unicode.org/iso15924/iso15924codes.html
            </script>
          </personalName>
          <gender>
            male, female, unknown
          </gender>
          <birthdate>
            YYYY-MM-DD
            생몰일은 입력하지 않으면 표시되지 않는다.
          </birthdate>
          <deathDate>
            YYYY-MM-DD
          </deathDate>
          <dateType>
            연도가 명확하지 않을 때 표시함
          </dateType>
          <nationality>
            https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2
            국가코드
          </nationality>
          <resource>
            <creationClass>
              Data Element Values Doc 참조
            </creationClass>
            <creationRole>
              Data Element Values Doc 참조
            </creationRole>
            <fieldOfCreation>
              <fieldType>
                듀이 십진분류법이나 키워드, 키 프레이즈 등 fieldOfCreationValue
                값에 대한 타입 설명
              </fieldType>
              <fieldOfCreationValue>
                듀이 십진분류법 코드나 키워드. fieldType에서 지정한 속성의 구체적인 값.
              </fieldOfCreationValue>
            </fieldOfCreation>
            <titleOfWork>
              <title>
                작업물의 이름. 시리즈 명이나 잡지명 등은 쓰지 않는다. contributedTo를 사용.
              </title>
              <imprint>
                <publisher>
                  퍼블리셔 명
                </publisher>
                <date>
                  YYYY, YYYY-MM, YYYY-MM-DD 같은 포맷
                </date>
              </imprint>
              <identifier>
                <identifierValue>
                  13자리 ISBN 등
                </identifierValue>
                <identifierType>
                  identifier의 타입 설명. ISBN, ISTC, ISRC 등등
                </identifierType>
              </identifier>
            </titleOfWork>
          </resource>
          <contributedTo>
            <titleOfCollectiveWorkOrWorkPerformed>
            </titleOfCollectiveWorkOrWorkPerformed>
            <identifier>
              <identifierType>
              </identifierType>
              <identifierValue>
              </identifierValue>
            </identifier>
          </contributedTo>
          <personalNameVariant>
            한 identifer가 personalName을 여러 개 가지고 있을 경우
            위의 <personalNameVariant>와 구조가 완전히 같다.
          </personalNameVariant>
          <instrumentAndVoice>
            악기연주인지 목소리인지를 Data element값으로 표현
          </instrumentAndVoice>
        </personOrFiction>
        /* organisation의 경우 */
        <organisation>
          <organisationType>
             ISNI Data element values Doc 참조
             University, College, Publisher 등등이 가능
          </organisationType>
          <organisationName>
            <mainName>
              가장 흔히 사용되는 조직명
            </mainName>
            <subdivisionName>
              부서 / 하부조직명
            </subdivisionName>
          </organisationName>
          <usageDateFrom>
            YYYY-MM-DD
          </usageDateFrom>
          <usageDateTo>
            YYYY-MM-DD
          </usageDateTo>
          <location>
            <countryCode>
              다국적 조직의 경우 메인 오피스가 있는 국가코드를 포함
            </countryCode>
            <locode>
            </locode>
            <regionOrState>
            </regionOrState>
            <city>
            </city>
          </location>
          <resource>
          </resource>
          <organisationNameVariant>
          </organisationNameVariant>
        </organisation>
      </identity>
      <languageOfIdentity>
        ISO 639-2 http://id.loc.gov/vocabulary/iso639-2 에 따른 언어
      </languageOfIdentity>
      <countriesAssociated>
        <countryCode>
          ISO 3166-1 2 글자 코드 http://en.wikipedia.org/wiki/ISO_31661_alpha-2
        </countryCode>
        <regionOrState>
          ISO 3166-2 코드 http://en.wikipedia.org/wiki/ISO_3166-2
        </regionOrState>
        <city>
          가능하면 UN/LOCODE를 사용하고 그렇지 않으면 자유 입력
          http://www.unece.org/cefact/locode/service/location.htm
        </city>
      </countriesAssociated>
      <externalInformation>
        <source>
          인용의 출처
        </source>
        <information>
          웹 페이지에서 찾을 수 있는 정보의 성격. Wikipedia Page, IMDB page 등.
        </information>
        <URI>
        </URI>
      </externalInformation>
      <note>
        Identity에 대한 자유 형식의 추가 text
      </note>
    </identityInformation>
    <isNot>
      <identityType>
        personOrFiction  OR organisation
      </identityType>
      <ISNI>
        16자리 ISNI 코드
        만약 이 값이 없다면 <noISNI>가 있어야 한다.
      </ISNI>
      <noISNI>
        만약 이 필드가 없다면 <ISNI>가 있어야 한다.
      </noISNI>
      <PPN>
        ISNI 데이터베이스 식별자. 9글자의 문자열.
      </PPN>
      <personalName>
        위의 personalName 구조를 따른다. organisationName과 둘 중 하나만 가능하며, 둘 중 하나는 반드시 포함되어야 한다.
      </personalName>
      <organisationName>
        위의 organisationName 구조를 따른다. personalName과 둘 중 하나만 가능하며, 둘 중 하나는 반드시 포함되어야 한다.
      </organisationName>
    </isNot>
    <isRelated identityType="">
      <relationType>
         ISNI data element values doc 참고
         co-author, pseud, supersedes 등이 가능
      </relationType>
      <ISNI>
        아래의 <noISNI>와 양자택일. 둘 중 하나는 반드시 포함되어야 한다.
      </ISNI>
      <noISNI>
        <PPN>
          상동
        </PPN>
        <personalName>
          상동. 아래의 <organisationName>과 양자택일
        </personalName>
        <organisationName>
          상동. 위의 <personalName>과 양자택일
        </organisationName>
        <relationQualification>
          관계를 명확히 하기 위해 사용됨. 연구소, 학부 등.
        </relationQualification>
        <startDateOfRelationship>
          YYYY-MM-DD
        </startDateOfRelationship>
        <endDateOfRelationship>
          YYYY-MM-DD
        </endDateOfRelationship>
      </noISNI>
    </isRelated>
    <merge>
      <mergeInstruction>
        M - Merge 요청 / P - 매뉴얼 리뷰 요청(드물게 사용됨) / N - 타겟 데이터베이스의 정보에 일치하는 field가 있다면 false(드물게 사용됨)
      </mergeInstruction>
      <mergeToPPN>
        이 항목 또는 <mergeToISNI> 둘 중 하나는 반드시 포함되어야 한다
      </mergeToPPN>
      <mergeToISNI>
        이 항목 또는 <mergeToPPN> 둘 중 하나는 반드시 포함되어야 한다
      </mergeToISNI>
    </merge>
  </Request>
{% endhighlight %}

### 결론

복잡해...

참고로 아래 오픈소스에서 루비로 된 XML 빌더를 발견할 수 있다.
[berkmancenter/author_names][ruby_isni_request_xml]

[ruby_isni_request_xml]:https://github.com/berkmancenter/author_names/blob/master/app/views/responses/isni.xml.builder
