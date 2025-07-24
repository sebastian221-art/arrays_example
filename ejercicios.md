// Métodos de ordenamiento en arrays - C# // 

using System;

class Program { static void Main() { Console.WriteLine("Métodos de Ordenamiento en Arrays:\n");

int[] datosOriginales = { 5, 2, 8, 3, 1 };

    int[] arrBubble = (int[])datosOriginales.Clone();
    BubbleSort(arrBubble);
    Console.WriteLine("1. Bubble Sort:     " + string.Join(", ", arrBubble));

    int[] arrSelection = (int[])datosOriginales.Clone();
    SelectionSort(arrSelection);
    Console.WriteLine("2. Selection Sort:  " + string.Join(", ", arrSelection));

    int[] arrInsertion = (int[])datosOriginales.Clone();
    InsertionSort(arrInsertion);
    Console.WriteLine("3. Insertion Sort:  " + string.Join(", ", arrInsertion));

    int[] arrQuick = (int[])datosOriginales.Clone();
    QuickSort(arrQuick, 0, arrQuick.Length - 1);
    Console.WriteLine("4. Quick Sort:      " + string.Join(", ", arrQuick));

    int[] arrMerge = (int[])datosOriginales.Clone();
    MergeSort(arrMerge, 0, arrMerge.Length - 1);
    Console.WriteLine("5. Merge Sort:      " + string.Join(", ", arrMerge));

    int[] arrDotNet = (int[])datosOriginales.Clone();
    Array.Sort(arrDotNet); // Usa un algoritmo interno muy optimizado
    Console.WriteLine("6. Array.Sort:      " + string.Join(", ", arrDotNet));
}

// 1. Bubble Sort
static void BubbleSort(int[] arr)
{
    for (int i = 0; i < arr.Length - 1; i++)
    {
        for (int j = 0; j < arr.Length - i - 1; j++)
        {
            if (arr[j] > arr[j + 1])
            {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}
//  Explicación: Compara elementos vecinos y los intercambia si están en el orden incorrecto. Es simple pero lento.

// 2. Selection Sort
    static void SelectionSort(int[] arr)
    {
        for (int i = 0; i < arr.Length - 1; i++)
        {
            int min = i;
            for (int j = i + 1; j < arr.Length; j++)
            {
                if (arr[j] < arr[min])
                    min = j;
            }
            int temp = arr[min];
            arr[min] = arr[i];
            arr[i] = temp;
        }
    }
    //  Explicación: Encuentra el menor elemento y lo coloca al principio. Se repite para cada posición.

    // 3. Insertion Sort
    static void InsertionSort(int[] arr)
    {
        for (int i = 1; i < arr.Length; i++)
        {
            int key = arr[i];
            int j = i - 1;
            while (j >= 0 && arr[j] > key)
            {
                arr[j + 1] = arr[j];
                j--;
            }
            arr[j + 1] = key;
        }
    }
    //  Explicación: Inserta cada elemento en su posición correcta como si estuvieras ordenando cartas a mano.

    // 4. Quick Sort
    static void QuickSort(int[] arr, int left, int right)
    {
        if (left < right)
        {
            int pivot = arr[(left + right) / 2];
            int i = left, j = right;
            while (i <= j)
            {
                while (arr[i] < pivot) i++;
                while (arr[j] > pivot) j--;
                if (i <= j)
                {
                    int temp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = temp;
                    i++; j--;
                }
            }
            QuickSort(arr, left, j);
            QuickSort(arr, i, right);
        }
    }

    //  Explicación: Usa un elemento pivote para dividir el array y ordenar recursivamente cada parte.

    // 5. Merge Sort
    static void MergeSort(int[] arr, int left, int right)
    {
        if (left < right)
        {
            int mid = (left + right) / 2;
            MergeSort(arr, left, mid);
            MergeSort(arr, mid + 1, right);
            Merge(arr, left, mid, right);
        }
    }

    static void Merge(int[] arr, int left, int mid, int right)
    {
        int[] temp = new int[right - left + 1];
        int i = left, j = mid + 1, k = 0;

        while (i <= mid && j <= right)
        {
            if (arr[i] <= arr[j])
                temp[k++] = arr[i++];
            else
                temp[k++] = arr[j++];
        }

        while (i <= mid) temp[k++] = arr[i++];
        while (j <= right) temp[k++] = arr[j++];

        for (i = left; i <= right; i++)
            arr[i] = temp[i - left];
    }
    //  Explicación: Divide el array en mitades y