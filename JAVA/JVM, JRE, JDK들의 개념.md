# JVM, JRE, JDK 개념과 차이점 정리

## 🖥️ JVM(Java Virtual Machine) - 자바 가상 머신

- 자바는 C와 같은 기존의 컴파일 언어와 다르다.
- C로 짠 코드를 윈도우 용으로 컴파일 한 것을 맥이나 리눅스 같은 다른 OS에서 실행할 수 없음.
- 따라서 다양한 OS용으로 따로 컴파일 해야 해서 번거로움.
- JVM은 각 OS에 맞는 기계어와 자바 바이트코드를 읽을 수 있다.
- 자바는 자바 바이트코드로 컴파일이 된다.
- JVM은 컴파일된 자바 바이트코드를 읽고 다양한 OS에 맞게 실행해 주는 역할을 한다.
- 코틀린, 스칼라, 그루비 등 몇몇 다른 언어들에서도 사용가능
- 주요 기능:
  - 바이트코드 실행
  - 메모리 관리 및 가비지 컬렉션(GC)
  - 실행 환경 제공 (스레드 관리 등)

## ☕ JRE (Java Runtime Environment) - 자바 실행 환경

- JRE는 **JVM + 실행에 필요한 라이브러리**를 포함한 환경이다.
- 자바 애플리케이션을 실행할 수 있도록 필요한 요소들이 포함됨.
- 과거에는 따로 JRE를 설치해야 했지만, JDK만 설치해도 된다.
- **JRE에는 개발 도구가 포함되지 않음!** (컴파일 불가)

## 🏗️ JDK (Java Development Kit) - 자바 개발 키트

- JDK는 **JRE + 개발 도구(컴파일러, 디버거 등)**가 포함된 패키지다.
- 오라클은 자바 11부터 JDK만 제공하고 JRE를 따로 제공하지 않는다.
- 주요 구성 요소:
  - JRE (JVM + 실행 라이브러리)
  - `javac` (컴파일러)
  - `java` (실행 명령어)
  - `jdb` (디버거)
  - `jar` (JAR 파일 생성 도구)

## 📌 JVM, JRE, JDK 차이점 비교

| 구분           | JVM (Java Virtual Machine)               | JRE (Java Runtime Environment) | JDK (Java Development Kit)                            |
| -------------- | ---------------------------------------- | ------------------------------ | ----------------------------------------------------- |
| 역할           | 바이트코드 실행                          | 실행 환경 제공                 | 개발 환경 제공                                        |
| 포함 요소      | - JVM만 포함                             | - JVM + 라이브러리             | - JRE + 개발 도구                                     |
| 실행 가능 여부 | ❌ (단독 실행 불가)                      | ✅ (실행 가능)                 | ✅ (개발 및 실행 가능)                                |
| 주요 구성 요소 | - 클래스 로더 <br> - 실행 엔진 <br> - GC | - JVM <br> - 실행 라이브러리   | - JRE <br> - `javac` (컴파일러) <br> - `jdb` (디버거) |
| 대상           | OS에 상관없이 자바 실행                  | 자바 실행 환경 제공            | 자바 개발 및 실행 가능                                |
| 필요 여부      | JRE/JDK 내부에서 동작                    | 실행만 필요할 경우 설치        | 개발할 경우 반드시 설치                               |

---

# ☕ JDK 다운로드 및 오라클 유료/무료 JDK 비교

### 🔹 유료 JDK (Oracle JDK)

- **기업용 라이선스가 필요**하며, 비용을 지불해야 함.
- 장기 지원(LTS) 및 **보안 업데이트를 제공**.
- **기업 환경에서 운영 목적으로 사용하면 유료** (개인 개발 및 학습용으로는 무료).
- SLA(서비스 수준 계약) 기반의 공식 기술 지원 포함.

📌 **Oracle JDK 라이선스 정책**

- Java 17부터는 **무료 사용 가능** (GPL 기반).
- Java 8, 11 등 구버전은 **기업 환경에서 사용 시 유료**.

### 🔹 무료 JDK (OpenJDK)

- **오픈소스 기반의 무료 JDK**.
- 오라클 JDK와 기능적으로 동일하지만, **6개월마다 새 버전이 출시됨**.
- **보안 패치 및 장기 지원이 부족할 수 있음**.

📌 **대표적인 무료 JDK**

- **Oracle OpenJDK** (오라클 제공)
- **Eclipse Temurin (Adoptium)** (많이 사용됨)
- **Amazon Corretto** (AWS 제공, 장기 지원 포함)
- **Azul Zulu** (무료 및 유료 지원 옵션 제공)
- **Microsoft Build of OpenJDK** (Azure 환경 최적화)

## 오라클 이외의 무료 JDK 배포판 비교

| JDK 배포판                     | 제공 업체          | 특징                                                    |
| ------------------------------ | ------------------ | ------------------------------------------------------- |
| **OpenJDK**                    | Oracle             | 공식 오픈소스 JDK, 6개월마다 새 버전 출시               |
| **Eclipse Temurin (Adoptium)** | Eclipse Foundation | 가장 많이 사용되는 무료 JDK, 기업에서도 안정적으로 사용 |
| **Amazon Corretto**            | Amazon AWS         | 장기 지원(LTS) 제공, AWS 환경 최적화                    |
| **Azul Zulu**                  | Azul               | 무료 및 유료 지원 옵션 제공                             |
| **Microsoft Build of OpenJDK** | Microsoft          | Azure 및 Windows 환경 최적화                            |
| **GraalVM**                    | Oracle             | 성능 최적화, 네이티브 이미지 지원                       |

✅ **기업 환경**에서는 **Eclipse Temurin** 또는 **Amazon Corretto**가 많이 사용됨.  
✅ **AWS 사용 시** Amazon Corretto, **Azure 사용 시** Microsoft Build of OpenJDK 추천.  
✅ **일반 개발자는 OpenJDK 또는 Eclipse Temurin을 사용하면 무난함**.
