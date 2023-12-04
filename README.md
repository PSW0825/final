#include <stdio.h>

int main(int argc, char *argv[]) {
    FILE *source, *destination;
    char ch;

    // 명령행 매개변수가 충분하지 않을 경우 에러 메시지 출력
    if (argc != 3) {
        printf("Usage: %s <source_file> <destination_file>\n", argv[0]);
        return 1;  // 프로그램 종료
    }

    // 소스 파일 열기
    source = fopen(argv[1], "rb");
    if (source == NULL) {
        perror("Error opening source file");
        return 2;
    }

    // 대상 파일 열기 (이미 존재할 경우 덮어쓰기)
    destination = fopen(argv[2], "wb");
    if (destination == NULL) {
        perror("Error opening destination file");
        fclose(source);
        return 3;
    }

    // 파일 내용 복사
    while ((ch = fgetc(source)) != EOF) {
        fputc(ch, destination);
    }

    // 파일 닫기
    fclose(source);
    fclose(destination);

    printf("File copy successful.\n");

    return 0;
}

1. 코드 저장: 예를 들어, 'mycp.c'로 파일에 저장합니다.
2. 컴파일: 명령 프롬프트나 터미널에서 컴파일 명령을 실행합니다.
   gcc mycp.c -o mycp
   위 명령은 GCC 컴파일러를 사용하여 'mycp.c'를 'mycp'라는 실행 파일로 컴파일합니다.
3. 실행: 컴파일이 성공하면, 명령행에서 다음과 같이 프로그램을 실행할 수 있습니다.
   ./mycp f1.txt f2.txt
   여기서 'f1.txt'는 소스 파일이고, 'f2.txt'는 대상 파일입니다. 주어진 예제에서는 './'를 사용하여 현재 디렉토리에서 실행파일을 찾도     록 했지만, 환경에 따라서는 경로를 추가해주어야 할 수도 있습니다.
