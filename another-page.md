{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 12,
   "id": "04e95ca3",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "        Date  Week No  Year   Site       Date_TAG event_type    ent  tet_ent  \\\n",
      "0 2021-03-18       12  2021  BHL-5  BHL-5-12-2021       base  141.0     28.0   \n",
      "1 2021-03-18       12  2021     T8     T8-12-2021       base  126.0     16.0   \n",
      "2 2021-03-18       12  2021    S11    S11-12-2021       base   77.0     21.0   \n",
      "3 2021-03-18       12  2021   SW12   SW12-12-2021       base   20.0      0.0   \n",
      "4 2021-04-09       15  2021  BHL-5  BHL-5-15-2021       base   52.0      4.0   \n",
      "\n",
      "   tyl_ent  ecoli  Precip  Precip-1  Temp  Temp-1  TSS    DRP     TP      TN  \\\n",
      "0      6.0   79.0     NaN       0.0   NaN    26.3  NaN    NaN    NaN     NaN   \n",
      "1      1.0   75.0     NaN       NaN   NaN     NaN  0.5  0.083  0.087  16.402   \n",
      "2      2.0   10.0     NaN       NaN   NaN     NaN  0.5  0.028  0.033  18.149   \n",
      "3      0.0    3.0     NaN       NaN   NaN     NaN  3.0  0.002  0.027  10.910   \n",
      "4      1.0   16.0     0.0       NaN  67.4     NaN  NaN    NaN    NaN     NaN   \n",
      "\n",
      "   Avg_Flow  \n",
      "0       NaN  \n",
      "1  0.001087  \n",
      "2  0.022349  \n",
      "3  0.022349  \n",
      "4       NaN  \n"
     ]
    }
   ],
   "source": [
    "# Importing panda library\n",
    "import pandas as pd\n",
    "\n",
    "# Read the CSV file with a date column in the \"DD/MM/YYYY\" format\n",
    "df = pd.read_csv('../shbne/FIB/Mapped with NutrientsTIME.csv', parse_dates=['Date'], dayfirst=True)\n",
    "\n",
    "# Print the first few rows of the dataframe\n",
    "print(df.head())"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "id": "e0cf1d97",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "RangeIndex: 353 entries, 0 to 352\n",
      "Data columns (total 19 columns):\n",
      " #   Column      Non-Null Count  Dtype         \n",
      "---  ------      --------------  -----         \n",
      " 0   Date        353 non-null    datetime64[ns]\n",
      " 1   Week No     353 non-null    int64         \n",
      " 2   Year        353 non-null    int64         \n",
      " 3   Site        353 non-null    object        \n",
      " 4   Date_TAG    353 non-null    object        \n",
      " 5   event_type  353 non-null    object        \n",
      " 6   ent         324 non-null    float64       \n",
      " 7   tet_ent     324 non-null    float64       \n",
      " 8   tyl_ent     331 non-null    float64       \n",
      " 9   ecoli       318 non-null    float64       \n",
      " 10  Precip      330 non-null    float64       \n",
      " 11  Precip-1    330 non-null    float64       \n",
      " 12  Temp        330 non-null    float64       \n",
      " 13  Temp-1      330 non-null    float64       \n",
      " 14  TSS         247 non-null    float64       \n",
      " 15  DRP         247 non-null    float64       \n",
      " 16  TP          247 non-null    float64       \n",
      " 17  TN          247 non-null    float64       \n",
      " 18  Avg_Flow    247 non-null    float64       \n",
      "dtypes: datetime64[ns](1), float64(13), int64(2), object(3)\n",
      "memory usage: 52.5+ KB\n"
     ]
    }
   ],
   "source": [
    "# Checking if the data has been detected properly for date and time variable\n",
    "df.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "id": "c35aa8ab",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Index(['Date', 'Week No', 'Year', 'Site', 'Date_TAG', 'event_type', 'ent',\n",
       "       'tet_ent', 'tyl_ent', 'ecoli', 'Precip', 'Precip-1', 'Temp', 'Temp-1',\n",
       "       'TSS', 'DRP', 'TP', 'TN', 'Avg_Flow'],\n",
       "      dtype='object')"
      ]
     },
     "execution_count": 19,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Listing the columns for the read dataets\n",
    "df.columns"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "id": "bbe5e528",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Date</th>\n",
       "      <th>ent</th>\n",
       "      <th>tet_ent</th>\n",
       "      <th>tyl_ent</th>\n",
       "      <th>ecoli</th>\n",
       "      <th>Precip</th>\n",
       "      <th>Precip-1</th>\n",
       "      <th>Temp</th>\n",
       "      <th>Temp-1</th>\n",
       "      <th>TSS</th>\n",
       "      <th>DRP</th>\n",
       "      <th>TP</th>\n",
       "      <th>TN</th>\n",
       "      <th>Avg_Flow</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2021-03-18</td>\n",
       "      <td>141.0</td>\n",
       "      <td>28.0</td>\n",
       "      <td>6.0</td>\n",
       "      <td>79.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>0.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>26.3</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2021-03-18</td>\n",
       "      <td>126.0</td>\n",
       "      <td>16.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>75.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>0.5</td>\n",
       "      <td>0.083</td>\n",
       "      <td>0.087</td>\n",
       "      <td>16.402</td>\n",
       "      <td>0.001087</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>2021-03-18</td>\n",
       "      <td>77.0</td>\n",
       "      <td>21.0</td>\n",
       "      <td>2.0</td>\n",
       "      <td>10.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>0.5</td>\n",
       "      <td>0.028</td>\n",
       "      <td>0.033</td>\n",
       "      <td>18.149</td>\n",
       "      <td>0.022349</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>2021-03-18</td>\n",
       "      <td>20.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>3.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>3.0</td>\n",
       "      <td>0.002</td>\n",
       "      <td>0.027</td>\n",
       "      <td>10.910</td>\n",
       "      <td>0.022349</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>2021-04-09</td>\n",
       "      <td>52.0</td>\n",
       "      <td>4.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>16.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>67.4</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>2021-04-09</td>\n",
       "      <td>888.0</td>\n",
       "      <td>125.0</td>\n",
       "      <td>39.0</td>\n",
       "      <td>1000.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>67.4</td>\n",
       "      <td>67.4</td>\n",
       "      <td>0.5</td>\n",
       "      <td>0.081</td>\n",
       "      <td>0.085</td>\n",
       "      <td>20.973</td>\n",
       "      <td>0.012124</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>6</th>\n",
       "      <td>2021-04-09</td>\n",
       "      <td>88.0</td>\n",
       "      <td>14.0</td>\n",
       "      <td>3.0</td>\n",
       "      <td>40.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>67.4</td>\n",
       "      <td>67.4</td>\n",
       "      <td>2.0</td>\n",
       "      <td>0.015</td>\n",
       "      <td>0.021</td>\n",
       "      <td>25.343</td>\n",
       "      <td>0.009243</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>7</th>\n",
       "      <td>2021-04-09</td>\n",
       "      <td>6.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>4.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>67.4</td>\n",
       "      <td>67.4</td>\n",
       "      <td>6.0</td>\n",
       "      <td>0.001</td>\n",
       "      <td>0.031</td>\n",
       "      <td>10.290</td>\n",
       "      <td>0.073479</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>8</th>\n",
       "      <td>2021-04-15</td>\n",
       "      <td>38.0</td>\n",
       "      <td>3.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>16.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>0.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>67.4</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>9</th>\n",
       "      <td>2021-04-15</td>\n",
       "      <td>172.0</td>\n",
       "      <td>3.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>380.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>0.5</td>\n",
       "      <td>0.049</td>\n",
       "      <td>0.047</td>\n",
       "      <td>21.386</td>\n",
       "      <td>0.004176</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "        Date    ent  tet_ent  tyl_ent   ecoli  Precip  Precip-1  Temp  Temp-1  \\\n",
       "0 2021-03-18  141.0     28.0      6.0    79.0     NaN       0.0   NaN    26.3   \n",
       "1 2021-03-18  126.0     16.0      1.0    75.0     NaN       NaN   NaN     NaN   \n",
       "2 2021-03-18   77.0     21.0      2.0    10.0     NaN       NaN   NaN     NaN   \n",
       "3 2021-03-18   20.0      0.0      0.0     3.0     NaN       NaN   NaN     NaN   \n",
       "4 2021-04-09   52.0      4.0      1.0    16.0     0.0       NaN  67.4     NaN   \n",
       "5 2021-04-09  888.0    125.0     39.0  1000.0     0.0       0.0  67.4    67.4   \n",
       "6 2021-04-09   88.0     14.0      3.0    40.0     0.0       0.0  67.4    67.4   \n",
       "7 2021-04-09    6.0      1.0      0.0     4.0     0.0       0.0  67.4    67.4   \n",
       "8 2021-04-15   38.0      3.0      0.0    16.0     NaN       0.0   NaN    67.4   \n",
       "9 2021-04-15  172.0      3.0      1.0   380.0     NaN       NaN   NaN     NaN   \n",
       "\n",
       "   TSS    DRP     TP      TN  Avg_Flow  \n",
       "0  NaN    NaN    NaN     NaN       NaN  \n",
       "1  0.5  0.083  0.087  16.402  0.001087  \n",
       "2  0.5  0.028  0.033  18.149  0.022349  \n",
       "3  3.0  0.002  0.027  10.910  0.022349  \n",
       "4  NaN    NaN    NaN     NaN       NaN  \n",
       "5  0.5  0.081  0.085  20.973  0.012124  \n",
       "6  2.0  0.015  0.021  25.343  0.009243  \n",
       "7  6.0  0.001  0.031  10.290  0.073479  \n",
       "8  NaN    NaN    NaN     NaN       NaN  \n",
       "9  0.5  0.049  0.047  21.386  0.004176  "
      ]
     },
     "execution_count": 23,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Dropping extra time related columns and variable \"event_type\" and \"Site\"\n",
    "df2=df.drop([\"Week No\", \"Year\", \"Date_TAG\", \"event_type\", \"Site\"], axis=1)\n",
    "df2.head(10)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 41,
   "id": "b424b07a",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Index(['Date', 'ent', 'tet_ent', 'tyl_ent', 'ecoli', 'Precip', 'Precip-1',\n",
       "       'Temp', 'Temp-1', 'TSS', 'DRP', 'TP', 'TN', 'Avg_Flow'],\n",
       "      dtype='object')"
      ]
     },
     "execution_count": 41,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df2.columns"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 79,
   "id": "a6ff9737",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>ent</th>\n",
       "      <th>tyl_ent</th>\n",
       "      <th>ecoli</th>\n",
       "      <th>tet_ent</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>141.0</td>\n",
       "      <td>6.0</td>\n",
       "      <td>79.0</td>\n",
       "      <td>28.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>126.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>75.0</td>\n",
       "      <td>16.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>77.0</td>\n",
       "      <td>2.0</td>\n",
       "      <td>10.0</td>\n",
       "      <td>21.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>20.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>3.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>52.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>16.0</td>\n",
       "      <td>4.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "     ent  tyl_ent  ecoli  tet_ent\n",
       "0  141.0      6.0   79.0     28.0\n",
       "1  126.0      1.0   75.0     16.0\n",
       "2   77.0      2.0   10.0     21.0\n",
       "3   20.0      0.0    3.0      0.0\n",
       "4   52.0      1.0   16.0      4.0"
      ]
     },
     "execution_count": 79,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# For this problem, we are tryign to establish an ML model to predict the variable \"tet_ent\" from the other phenotypic variables only\n",
    "df3 = df2[['ent', 'tyl_ent', 'ecoli','tet_ent']]\n",
    "df3.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 94,
   "id": "8ce54ab5",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "ent        29\n",
      "tyl_ent    22\n",
      "ecoli      35\n",
      "tet_ent    29\n",
      "dtype: int64\n"
     ]
    }
   ],
   "source": [
    "# Checking null values\n",
    "print(df3.isna().sum())\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 95,
   "id": "5c653759",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "ent        0\n",
      "tyl_ent    0\n",
      "ecoli      0\n",
      "tet_ent    0\n",
      "dtype: int64\n"
     ]
    }
   ],
   "source": [
    "#dropping null values where ecoli or ent was not present\n",
    "df4 = df3.dropna(subset=['ecoli', 'ent'])\n",
    "print(df4.isna().sum())"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 96,
   "id": "a8050f97",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Subsetting data for ML model\n",
    "X = df4.iloc[:,:-1]\n",
    "y = df4.iloc[:,-1]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 97,
   "id": "fa7a2fb7",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Importing scikitlearn's train-test split module\n",
    "from sklearn.model_selection import train_test_split\n",
    "X_train, X_test, y_train, y_test = train_test_split(X,y,random_state=100)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 98,
   "id": "846d0212",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Importing the XGBoost Regression Model library\n",
    "from xgboost import XGBRegressor\n",
    "xg_reg = XGBRegressor()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 100,
   "id": "18e6c0d3",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "XGBRegressor(base_score=None, booster=None, callbacks=None,\n",
       "             colsample_bylevel=None, colsample_bynode=None,\n",
       "             colsample_bytree=None, early_stopping_rounds=None,\n",
       "             enable_categorical=False, eval_metric=None, feature_types=None,\n",
       "             gamma=None, gpu_id=None, grow_policy=None, importance_type=None,\n",
       "             interaction_constraints=None, learning_rate=None, max_bin=None,\n",
       "             max_cat_threshold=None, max_cat_to_onehot=None,\n",
       "             max_delta_step=None, max_depth=None, max_leaves=None,\n",
       "             min_child_weight=None, missing=nan, monotone_constraints=None,\n",
       "             n_estimators=100, n_jobs=None, num_parallel_tree=None,\n",
       "             predictor=None, random_state=None, ...)"
      ]
     },
     "execution_count": 100,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Fitting the model on training data\n",
    "xg_reg.fit(X_train, y_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 101,
   "id": "6dc38b0a",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Extracting predictions to a variable\n",
    "y_pred = xg_reg.predict(X_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 103,
   "id": "a7e5fa5c",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([ 1.14234976e-01,  2.51183567e+01,  1.62706314e+02,  1.04900894e+01,\n",
       "        1.35204611e+01,  2.74422264e+00,  8.50849915e+00,  2.15803790e+00,\n",
       "        1.60005894e+01,  4.11276484e+00,  3.09301959e-03,  6.30827367e-01,\n",
       "        9.16125031e+01,  6.76162148e+00,  5.77659726e-01,  1.60611224e+00,\n",
       "        1.68961945e+02,  6.32358322e+01,  4.74116474e-01,  1.07029028e+01,\n",
       "        2.02977061e+00,  6.16698027e-01, -2.33539119e-02,  1.87106967e+00,\n",
       "        2.77033663e+00,  1.75558910e+01,  1.29113197e+00,  1.34016352e+01,\n",
       "        2.77310282e-01,  3.19073987e+00,  9.35235202e-01,  9.37408161e+00,\n",
       "        1.78176260e+00,  1.25985823e+01,  5.56197286e-01,  6.81739300e-02,\n",
       "        4.36599255e+00,  1.86653748e+01,  7.22506571e+00,  7.21465528e-01,\n",
       "        1.59385252e+01,  4.65708748e-02,  2.13789201e+00,  1.81671448e+01,\n",
       "        2.41955185e+01,  1.55449314e+01,  6.53553104e+00,  9.50714588e+00,\n",
       "        4.26936874e+01,  9.84724426e+01,  2.17736263e+01,  1.02943239e+01,\n",
       "        6.91888869e-01,  3.00330334e+01,  3.23441124e+01,  1.43518038e+01,\n",
       "        8.41244042e-01,  4.89130592e+00,  9.14814224e+01,  1.66347103e+01,\n",
       "        1.44039581e+02,  6.67873459e+01,  1.17223576e-01,  3.93083191e+01,\n",
       "        1.00113115e+01,  9.96158386e+02,  9.21342468e+00,  6.40713155e-01,\n",
       "        3.76749396e-01,  4.37936163e+00,  3.09301959e-03,  3.28206367e+01,\n",
       "        9.89186287e-01,  2.99593091e-01,  2.22383308e+01,  6.76162148e+00,\n",
       "        1.08662539e+01,  3.81946135e+00,  6.40713155e-01], dtype=float32)"
      ]
     },
     "execution_count": 103,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "y_pred"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 107,
   "id": "55682baa",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "1209.7886102460598\n"
     ]
    }
   ],
   "source": [
    "# Checking model performance with MSE and RMSE\n",
    "from sklearn.metrics import mean_squared_error\n",
    "mse = mean_squared_error(y_test, y_pred)\n",
    "print(mse)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 109,
   "id": "b7fd76c2",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.9138017541278903"
      ]
     },
     "execution_count": 109,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Checking model performance with r2\n",
    "\n",
    "from sklearn.metrics import r2_score\n",
    "r2_score(y_test, y_pred)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 110,
   "id": "607d0982",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAkQAAAGwCAYAAABIC3rIAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjUuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8qNh9FAAAACXBIWXMAAA9hAAAPYQGoP6dpAAA71klEQVR4nO3deXhU5f3//9eQZbKQDCQhCYGAQWIBww6CgBBZrbL4w48gmyhYcAGMgCxVC/JRIliBKoJLWRQXrAUsH2spqVYggEIDkUXcMGxCGpCQhSwDyfn9wZdphwTMwExmwnk+rmuui7nPPWfe547tvK77nHMfi2EYhgAAAEyslrcLAAAA8DYCEQAAMD0CEQAAMD0CEQAAMD0CEQAAMD0CEQAAMD0CEQAAMD1/bxdQU5SXl+v48eMKCwuTxWLxdjkAAKAKDMNQQUGB4uLiVKvW5eeBCERVdPz4ccXHx3u7DAAAcBWOHj2qhg0bXnY7gaiKwsLCJF0Y0PDwcC9XAwAAqiI/P1/x8fGO3/HLIRBV0cXTZOHh4QQiAABqmF+63IWLqgEAgOkRiAAAgOkRiAAAgOkRiAAAgOkRiAAAgOkRiAAAgOkRiAAAgOkRiAAAgOkRiAAAgOl5NRBt3rxZAwYMUFxcnCwWiz766COn7YZhaPbs2YqLi1NwcLCSk5O1f/9+pz6lpaWaOHGioqKiFBoaqoEDB+rYsWNOfXJzczVq1CjZbDbZbDaNGjVKZ86c8fDRAQCAmsKrgejs2bNq3bq1Fi9eXOn2+fPna8GCBVq8eLF27typ2NhY9enTRwUFBY4+KSkpWrdunVavXq309HQVFhaqf//+Kisrc/QZPny4MjMztWHDBm3YsEGZmZkaNWqUx48PAABcWV6RXQdzCrX7SK4OnixUXpHdK3VYDMMwvPLNl7BYLFq3bp3uvvtuSRdmh+Li4pSSkqLp06dLujAbFBMTo3nz5mn8+PHKy8tTvXr1tGrVKg0dOlTSf55K/8knn6hfv346cOCAWrRooS+++EKdOnWSJH3xxRe69dZb9c033+hXv/pVlerLz8+XzWZTXl4ezzIDAMANjp8p1vQ1e7Tl+1OOtu6JUXrhnlaKqxPslu+o6u+3z15DlJWVpezsbPXt29fRZrVa1aNHD23btk2SlJGRoXPnzjn1iYuLU1JSkqPP9u3bZbPZHGFIkjp37iybzeboU5nS0lLl5+c7vQAAgHvkFdkrhCFJ2vz9Kc1Ys6faZ4p8NhBlZ2dLkmJiYpzaY2JiHNuys7MVGBiounXrXrFPdHR0hf1HR0c7+lQmNTXVcc2RzWZTfHz8NR0PAAD4j1OF9gph6KLN35/SqUICkROLxeL03jCMCm2XurRPZf1/aT8zZ85UXl6e43X06FEXKwcAAJeTX3LuitsLfmG7u/lsIIqNjZWkCrM4OTk5jlmj2NhY2e125ebmXrHPv//97wr7P3nyZIXZp/9mtVoVHh7u9AIAAO4RHhRwxe1hv7Dd3Xw2ECUkJCg2NlZpaWmONrvdrk2bNqlLly6SpPbt2ysgIMCpz4kTJ7Rv3z5Hn1tvvVV5eXnasWOHo8+XX36pvLw8Rx8AAFC9omoHqntiVKXbuidGKap2YLXW41+t33aJwsJC/fDDD473WVlZyszMVEREhBo1aqSUlBTNnTtXiYmJSkxM1Ny5cxUSEqLhw4dLkmw2m8aOHaspU6YoMjJSERERmjp1qlq2bKnevXtLkpo3b6477rhDv/nNb/T6669LksaNG6f+/ftX+Q4zAADgXraQQL1wTyvNWLNHmy+5y2zePa1kC6neQOTV2+4///xz3X777RXaR48erZUrV8owDD377LN6/fXXlZubq06dOunVV19VUlKSo29JSYmefPJJvffeeyouLlavXr20ZMkSp4ugT58+rUmTJmn9+vWSpIEDB2rx4sWqU6dOlWvltnsAANwvr8iuU4V2FZScU1hQgKJqB7o1DFX199tn1iHydQQiAABqnhq/DhEAAEB1IRABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADTIxABAADT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69tvv3XqYxiGZs+erbi4OAUHBys5OVn79+936lNaWqqJEycqKipKoaGhGjhwoI4dO1adh1KjpKamymKxKCUlxdHGOLvPTz/9pJEjRyoyMlIhISFq06aNMjIyHNsZ62t3/vx5Pf3000pISFBwcLCaNGmiOXPmqLy83NGHcXbd5s2bNWDAAMXFxcliseijjz5y2u6uMc3NzdWoUaNks9lks9k0atQonTlz5toPwIDXrF692ggICDDefPNN4+uvvzYef/xxIzQ01Dh8+LC3S6sR+vXrZ6xYscLYt2+fkZmZadx1111Go0aNjMLCQkefF154wQgLCzPWrFlj7N271xg6dKhRv359Iz8/39Hn4YcfNho0aGCkpaUZu3btMm6//XajdevWxvnz571xWD5tx44dxg033GC0atXKePzxxx3tjLN7nD592mjcuLHxwAMPGF9++aWRlZVl/OMf/zB++OEHRx/G+to999xzRmRkpPHxxx8bWVlZxocffmjUrl3bWLRokaMP4+y6Tz75xHjqqaeMNWvWGJKMdevWOW1315jecccdRlJSkrFt2zZj27ZtRlJSktG/f/9rrp9A5EW33HKL8fDDDzu1NWvWzJgxY4aXKqrZcnJyDEnGpk2bDMMwjPLyciM2NtZ44YUXHH1KSkoMm81mvPbaa4ZhGMaZM2eMgIAAY/Xq1Y4+P/30k1GrVi1jw4YN1XsAPq6goMBITEw00tLSjB49ejgCEePsPtOnTze6det22e2MtXvcddddxpgxY5zaBg8ebIwcOdIwDMbZHS4NRO4a06+//tqQZHzxxReOPtu3bzckGd9888011cwpMy+x2+3KyMhQ3759ndr79u2rbdu2eamqmi0vL0+SFBERIUnKyspSdna20xhbrVb16NHDMcYZGRk6d+6cU5+4uDglJSXxd7jEY489prvuuku9e/d2amec3Wf9+vXq0KGD7r33XkVHR6tt27Z68803HdsZa/fo1q2bPv30U3333XeSpK+++krp6em68847JTHOnuCuMd2+fbtsNps6derk6NO5c2fZbLZrHnce7uolp06dUllZmWJiYpzaY2JilJ2d7aWqai7DMDR58mR169ZNSUlJkuQYx8rG+PDhw44+gYGBqlu3boU+/B3+Y/Xq1crIyNC//vWvCtsYZ/f58ccftXTpUk2ePFm//e1vtWPHDk2aNElW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\n",
      "text/plain": [
       "<Figure size 640x480 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "#PLotting the predictions\n",
    "\n",
    "import matplotlib.pyplot as plt\n",
    "import seaborn as sns\n",
    "\n",
    "# y_true contains the true values of the target variable\n",
    "# y_pred contains the predicted values of the target variable\n",
    "sns.scatterplot(x=y_test, y=y_pred)\n",
    "plt.xlabel('Actual Values')\n",
    "plt.ylabel('Predicted Values')\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 112,
   "id": "62e3395c",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAlQAAAHFCAYAAAA0SmdSAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjUuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8qNh9FAAAACXBIWXMAAA9hAAAPYQGoP6dpAAA+Q0lEQVR4nO3de3zP9f//8fvbDu/ZbMNsZk6bQ85MNAltksMskQ5Eiw5KkTOFyqFESunTQUVNisiHfCUUzSFRInwcPqmcD0NymIzZ9n7+/ui398e7Ddv79dY2btfL5X2x9/P1fL1ej9dju2x3r9fr/X7bjDFGAAAAcFuxgi4AAACgqCNQAQAAWESgAgAAsIhABQAAYBGBCgAAwCICFQAAgEUEKgAAAIsIVAAAABYRqAAAACwiUAHXoenTp8tms+X6GDJkyFXZ544dOzR69Gjt3bv3qmzfir1798pms2n69OkFXYrbFi9erNGjRxd0GcB1y7ugCwBQcJKSklSzZk2XsYiIiKuyrx07dmjMmDGKi4tTZGTkVdmHu8qVK6d169apatWqBV2K2xYvXqy3336bUAUUEAIVcB2rW7euGjduXNBlWJKRkSGbzSZvb/d/ndntdt18880erOqfk5aWJn9//4IuA7jucckPwCXNmTNHTZs2VUBAgEqUKKG2bdtq06ZNLnM2bNigrl27KjIyUsWLF1dkZKTuv/9+7du3zzln+vTpuvfeeyVJLVu2dF5ezL7EFhkZqZ49e+bYf1xcnOLi4pzPV65cKZvNpo8//liDBw9W+fLlZbfb9dtvv0mSli9frlatWikoKEj+/v5q1qyZvvnmmyseZ26X/EaPHi2bzab//Oc/uvfeexUcHKzSpUtr0KBByszM1M6dO9WuXTsFBgYqMjJSEydOdNlmdq2ffPKJBg0apPDwcBUvXlyxsbE5eihJCxcuVNOmTeXv76/AwEC1bt1a69atc5mTXdNPP/2ke+65R6VKlVLVqlXVs2dPvf3225Lkcvk2+/Lq22+/rVtvvVVhYWEKCAhQvXr1NHHiRGVkZOTod926dfXjjz+qRYsW8vf3V5UqVTRhwgQ5HA6XuadOndLgwYNVpUoV2e12hYWFqX379vr555+dcy5cuKAXX3xRNWvWlN1uV2hoqB566CH9/vvvV/yeAEUNgQq4jmVlZSkzM9Plke2ll17S/fffr9q1a+uzzz7Txx9/rDNnzqhFixbasWOHc97evXtVo0YNTZ48WV999ZVefvllpaSk6KabbtLx48clSQkJCXrppZck/fXHfd26dVq3bp0SEhLcqnv48OHav3+/3n33XX3xxRcKCwvTJ598ojZt2igoKEgfffSRPvvsM5UuXVpt27bNU6i6lPvuu08NGjTQvHnz1KtXL73++usaOHCgOnXqpISEBH3++ee67bbb9PTTT2v+/Pk51h8xYoR2796tadOmadq0aTp8+LDi4uK0e/du55xZs2apY8eOCgoK0qeffqoPPvhAJ0+eVFxcnNasWZNjm507d1a1atU0d+5cvfvuu3ruued0zz33SJKzt+vWrVO5cuUkSbt27VK3bt308ccfa9GiRXrkkUf0yiuv6PHHH8+x7SNHjqh79+564IEHtHDhQsXHx2v48OH65JNPnHPOnDmj5s2b67333tNDDz2kL774Qu+++65uuOEGpaSkSJIcDoc6duyoCRMmqFu3bvryyy81YcIELVu2THFxcTp37pzb3xOgUDIArjtJSUlGUq6PjIwMs3//fuPt7W2eeuopl/XOnDljwsPDzX333XfJbWdmZpo///zTBAQEmDfeeMM5PnfuXCPJrFixIsc6lStXNj169MgxHhsba2JjY53PV6xYYSSZW2+91WXe2bNnTenSpU2HDh1cxrOyskyDBg1MTEzMZbphzJ49e4wkk5SU5BwbNWqUkWQmTZrkMjc6OtpIMvPnz3eOZWRkmNDQUNO5c+cctd54443G4XA4x/fu3Wt8fHzMo48+6qwxIiLC1KtXz2RlZTnnnTlzxoSFhZlbbrklR03PP/98jmPo06ePycuv9KysLJORkWFmzJhhvLy8zIkTJ5zLYmNjjSTzww8/uKxTu3Zt07ZtW+fzsWPHGklm2bJll9zPp59+aiSZefPmuYz/+OOPRpJ55513rlgrUJRwhgq4js2YMUM//vijy8Pb21tfffWVMjMz9eCDD7qcvfLz81NsbKxWrlzp3Maff/6pp59+WtWqVZO3t7e8vb1VokQJnT17Vv/973+vSt133323y/O1a9fqxIkT6tGjh0u9DodD7dq1048//qizZ8+6ta877rjD5XmtWrVks9kUHx/vHPP29la1atVcLnNm69atm2w2m/N55cqVdcstt2jFihWSpJ07d+rw4cNKTExUsWL/+5VcokQJ3X333fr++++VlpZ22eO/kk2bNunOO+9USEiIvLy85OPjowcffFBZWVn65ZdfXOaGh4crJibGZax+/foux7ZkyRLdcMMNuv322y+5z0WLFqlkyZLq0KGDy/ckOjpa4eHhLj9DwLWAm9KB61itWrVyvSn96NGjkqSbbrop1/Uu/sPfrVs3ffPNN3ruued00003KSgoSDabTe3bt79ql3WyL2X9vd7sy165OXHihAICAvK9r9KlS7s89/X1lb+/v/z8/HKMp6am5lg/PDw817EtW7ZIkv744w9JOY9J+usVlw6HQydPnnS58Ty3uZeyf/9+tWjRQjVq1NAbb7yhyMhI+fn5af369erTp0+O71FISEiObdjtdpd5v//+uypVqnTZ/R49elSnTp2Sr69vrsuzLwcD1woCFYAcypQpI0n697//rcqVK19y3unTp7Vo0SKNGjVKzzzzjHM8PT1dJ06cyPP+/Pz8lJ6enmP8+PHjzloudvEZn4vrffPNNy/5ar2yZcvmuR5POnLkSK5j2cEl+9/se48udvjwYRUrVkylSpVyGf/78V/OggULdPbsWc2fP9/le7l58+Y8b+PvQkNDdfDgwcvOKVOmjEJCQrR06dJclwcGBrq9f6AwIlAByKFt27by9vbWrl27Lnt5yWazyRgju93uMj5t2jRlZWW5jGXPye2sVWRkpP7zn/+4jP3yyy/auXNnroHq75o1a6aSJUtqx44d6tu37xXn/5M+/fRTDRo0yBmC9u3bp7Vr1+rBBx+UJNWoUUPly5fXrFmzNGTIEOe8s2fPat68ec5X/l3Jxf0tXry4czx7exd/j4wxmjp1qtvHFB8fr+eff17Jycm67bbbcp1zxx13aPbs2crKylKTJk3c3hdQVBCoAOQQGRmpsWPHauTIkdq9e7fatWunUqVK6ejRo1q/fr0CAgI0ZswYBQUF6dZbb9Urr7yiMmXKKDIyUqtWrdIHH3ygkiVLumyzbt26kqT3339fgYGB8vPzU1RUlEJCQpSYmKgHHnhATz75pO6++27t27dPEydOVGhoaJ7qLVGihN5880316NFDJ06c0D333KOwsDD9/vvv2rJli37//XdNmTLF023Kk2PHjumuu+5Sr169dPr0aY0aNUp+fn4aPny4pL8un06cOFHdu3fXHXfcoccff1zp6el65ZVXdOrUKU2YMCFP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QAUAAGARgQoAAMAiAhUAAIBFBCoAAACLCFQAAAAWEagAAAAsIlABAABYRKACAACwiEAFAABgEYEKAADAIgIVAACARQQqAAAAiwhUAAAAFhGoAAAALCJQAQAAWESgAgAAsIhABQAAYBGBCgAAwCICFQAAgEUEKgAAAIsIVAAAABYRqAAAACwiUAEAAFhEoAIAALCIQAUAAGARgQoAAMAiAhUAAIBFBCoAAACLCFQAAAAWEagAAAAsIlABAABYRKACAACwiEAFAABgEYEKAADAIgIVAACARQQqAAAAiwhUAAAAFhGoAAAALPIu6AKudU3Gf6NM74CCLqNIs3sZTYyR6o7+SulZtoIux217JyQUdAkAgKuEM1QAAAAWEagAAAAsIlABAABYVOQClc1m04IFCwq6DMBtU6ZMUf369RUUFKSgoCA1bdpUS5YscS6fP3++2rZtqzJlyshms2nz5s05trFr1y7dddddCg0NVVBQkO677z4dPXr0ivt+99139dhjjykwMFCNGjXSt99+68lDA4DrVoEGqri4OA0YMKAgS7iiyMhITZ48uaDLwDWkQoUKmjBhgjZs2KANGzbotttuU8eOHbV9+3ZJ0tmzZ9WsWTNNmDAh1/XPnj2rNm3ayGazKTk5Wd99950uXLigDh06yOFwXHK/c+bM0eDBg3Xvvfdq/fr1atGiheLj47V///6rcpwAcD3hVX7AP6xDhw4uz8eNG6cpU6bo+++/V506dZSYmChJ2rt3b67rf/fdd9q7d682bdqkoKAgSVJSUpJKly6t5ORk3X777bmu99prr+mhhx5S69atVatWLU2ePFlfffWVpkyZovHjx3vuAAHgOlRgZ6h69uypVatW6Y033pDNZpPNZpO3t7deffVVl3nbtm1TsWLFtGvXrnzv49ChQ+rSpYtKlSqlkJAQdezY0eWPVM+ePdWpUye9+uqrKleunEJCQtSnTx9lZGRI+usM2r59+zRw4EBnjYAnZWVlafbs2Tp79qyaNm2ap3XS09Nls9lkt9udY35+fipWrJjWrFmT6zoXLlzQxo0bc4StNm3aaO3ate4fAABAUgGeoXrjjTf0yy+/qG7duho7dqwk6YMPPlBSUpKGDBninPfhhx+qRYsWqlq1ar62n5aWppYtW6pFixZavXq1vL299eKLL6pdu3b6z3/+I19fX0nSihUrVK5cOa1YsUK//fabunTpoujoaPXq1Uvz589XgwYN9Nhjj6lXr16X3V96errS09Odz1NTUyVJ9mJGXl4mX7XDlb2Ycfm3qMoO6pK0detW3XrrrTp//rxKlCihuXPnqnr16i5zsr/OyMhwGW/UqJECAgI0dOhQvfDCCzLGaMSIEXI4HDp06JDL3GwpKSnKyspSSEiIzpw545xTpkwZpaSk5LoOLu/i7w+soZeeRT+tcbdvBRaogoOD5evrK39/f4WHh0uSHn74YY0aNUrr169XTEyMMjIy9Mknn+iVV17J9/Znz56tYsWKadq0ac4zS0lJSSpZsqRWrlypNm3aSJJKlSqlt956S15eXqpZs6YSEhL0zTffqFevXipdurS8vLwUGBjorPFSxo8frzFjxuQYf7ahQ/7+WfmuHzm90PjS9wcVBYsXL3Z+nZGRoVdffVVnz57VunXrlJiYqHHjxqlixYrOOdk3ma9Zs0aHDx922dbAgQP17rvv6q233pLNZlOLFi1UpUoVHTx40GU/2U6cOCFJ+vHHH1WzZk0tW7ZMkrRz506lpaXlug7yJruXsI5eehb9dE9aWppb6xWqe6jKlSunhIQEffjhh4qJidGiRYt0/vx53Xvvvfne1saNG/Xbb78pMDDQZfz8+fMulw/r1KkjLy8vlxq2bt2a7/0NHz5cgwYNcj5PTU1VxYoV9eKmYsr08brMmrgSezGjFxo79NyGYkp3FN3LrttGt811vF+/fmrXrp22bNmixx9/3DmefXm6efPmio6Odlmnffv2GjlypI4fPy5vb2+VLFlSFStWVGxsrNq3b59jHxcuXFCvXr1UuXJlSVLr1q3l4+Oj5cuXq0qVKrmug8vLyMjQsmXLnL2E++ilZ9FPa7KvMOVXoQpUkvToo48qMTFRr7/+upKSktSlSxf5+/vnezsOh0ONGjXSzJkzcywLDQ11fv33HzabzXbZV0pdit1ud7mnJVu6w6bMIvxxKYVJusNWpD965kq/2DIyMlzmZH/t4+NzyXXLlSsnSUpOTtaxY8d011135TrXx8dHjRo10sqVKxUfH+/c5jfffKOOHTvyS9eCy31/kD/00rPop3vc7VmBBipfX19lZbleDmvfvr0CAgI0ZcoULVmyRKtXr3Zr2zfeeKPmzJmjsLAw5yuhPFUjYMWIESMUHx+vihUr6syZM5o9e7ZWrlyppUuXSvrr8tz+/fudl/l27twpSQoPD3deek5KSlKtWrUUGhqqdevWqX///ho4cKBq1Kjh3E+rVq101113qW/fvpKkQYMGKTExUT4+PoqKilJSUpL279+v3r17/5OHDwDXpAJ9H6rIyEj98MMP2rt3r44fPy6HwyEvLy/17NlTw4cPV7Vq1fL8yqe/6969u8qUKaOOHTvq22+/1Z49e7Rq1Sr1799fBw8ezFeNq1ev1qFDh3T8+HG3agEudvToUSUmJqpGjRpq1aqVfvjhBy1dulStW7eWJC1cuFANGzZUQsJfH6bctWtXNWzYUO+++65zGzt37lSnTp1Uq1YtjR07ViNHjszxCtldu3a5/Mx26dJFkyZN0pw5c3TTTTdp9erVWrx4sfMyIADAfQV6hmrIkCHq0aOHateurXPnzmnPnj2KjIzUI488opdeekkPP/yw29v29/fX6tWr9fTTT6tz5846c+aMypcvr1atWuXrjNXYsWP1+OOPq2rVqkpPT5cxRfuVZih4H3zwwWWX9+zZUz179rzsnAkTJlzyjT+z5fY+Vr1791alSpXUvn17LgUAgAcVaKC64YYbtG7duhzjKSkp8vb21oMPPphjWX4CTXh4uD766KNLLp8+fXqOsb+/K/rNN9+sLVu25HmfAADg+lOobkpPT0/XgQMH9Nxzz+m+++5T2bJlC7okAACAKypUH4786aefqkaNGjp9+rQmTpx42bkvvfSSSpQokesjPj7+H6oYAACgkJ2hysu9I9l69+6t++67L9dlxYsX92BVAAAAl1eoAlV+lC5dWqVLly7oMq7oh+GtFBISUtBlFGkZGRlavHixto1uy43UAIBCqVBd8gMAACiKCFQAAAAWEagAAAAsIlABAABYRKACAACwiEAFAABgEYEKAADAIgIVAACARQQqAAAAiwhUAAAAFhGoAAAALCJQAQAAWESgAgAAsIhABQAAYBGBCgAAwCICFQAAgEUEKgAAAIsIVAAAABYRqAAAACwiUAEAAFhEoAIAALCIQAUAAGARgQoAAMAiAhUAAIBFBCoAAACLCFQAAAAWEagAAAAsIlABAABYRKACAACwiEAFAABgEYEKAADAIgIVAACARQQqAAAAiwhUAAAAFhGoAAAALCJQAQAAWESgAgAAsIhABQAAYBGBCgAAwCICFQAAgEUEKgAAAIsIVAAAABYRqAAAACwiUAEAAFhEoAIAALCIQAUAAGARgQoAAMAiAhUAAIBFBCoAAACLCFQAAAAWEagAAAAsIlABAABYRKACAACwiEAFAABgEYEKAADAIgIVAACARQQqAAAAiwhUAAAAFhGoAAAALCJQAQAAWESgAgAAsIhABQAAYBGBCgAAwCICFQAAgEUEKgAAAIsIVAAAABYRqAAAACwiUAEAAFhEoAIAALCIQAUAAGARgQoAAMAiAhUAAIBFBCoAAACLCFQAAAAWEagAAAAsIlABAABYRKACAACwiEAFAABgEYEKAADAIgIVAACARQQqAAAAi7wLuoBrlTFGknTmzBn5+PgUcDVFW0ZGhtLS0pSamkovLaKXnkMvPYdeehb9tCY1NVXS//6O5xWB6ir5448/JElRUVEFXAkAAMivM2fOKDg4OM/zCVRXSenSpSVJ+/fvz9c3BDmlpqaqYsWKOnDggIKCggq6nCKNXnoOvfQceulZ9NMaY4zOnDmjiIiIfK1HoLpKihX76/a04OBgfqA9JCgoiF56CL30HHrpOfTSs+in+9w5EcJN6QAAABYRqAAAACwiUF0ldrtdo0aNkt1uL+hSijx66Tn00nPopefQS8+inwXDZvL7ukAAAAC44AwVAACARQQqAAAAiwhUAAAAFhGoAAAALCJQXQXvvPOOoqKi5Ofnp0aNGunbb78t6JIKnfHjx+umm25SYGCgwsLC1KlTJ+3cudNljjFGo0ePVkREhIoXL664uDht377dZU56erqeeuoplSlTRgEBAbrzzjt18ODBf/JQCpXx48fLZrNpwIABzjH6mD+HDh3SAw88oJCQEPn7+ys6OlobN250LqefeZOZmalnn31WUVFRKl68uKpUqaKxY8fK4XA459DL3K1evVodOnRQRESEbDabFixY4LLcU307efKkEhMTFRwcrODgYCUmJurUqVNX+eiuYQYeNXv2bOPj42OmTp1qduzYYfr3728CAgLMvn37Crq0QqVt27YmKSnJbNu2zWzevNkkJCSYSpUqmT///NM5Z8KECSYwMNDMmzfPbN261XTp0sWUK1fOpKamOuf07t3blC9f3ixbtsz89NNPpmXLlqZBgwYmMzOzIA6rQK1fv95ERkaa+vXrm/79+zvH6WPenThxwlSuXNn07NnT/PDDD2bPnj1m+fLl5rfffnPOoZ958+KLL5qQkBCzaNEis2fPHjN37lxTokQJM3nyZOccepm7xYsXm5EjR5p58+YZSebzzz93We6pvrVr187UrVvXrF271qxdu9bUrVvX3HHHHf/UYV5zCFQeFhMTY3r37u0yVrNmTfPMM88UUEVFw7Fjx4wks2rVKmOMMQ6Hw4SHh5sJEyY455w/f94EBwebd9991xhjzKlTp4yPj4+ZPXu2c86hQ4dMsWLFzNKlS//ZAyhgZ86cMdWrVzfLli0zsbGxzkBFH/Pn6aefNs2bN7/kcvqZdwkJCebhhx92GevcubN54IEHjDH0Mq/+Hqg81bcdO3YYSeb77793zlm3bp2RZH7++eerfFTXJi75edCFCxe0ceNGtWnTxmW8TZs2Wrt2bQFVVTScPn1a0v8+VHrPnj06cuSISy/tdrtiY2Odvdy4caMyMjJc5kRERKhu3brXXb/79OmjhIQE3X777S7j9DF/Fi5cqMaNG+vee+9VWFiYGjZsqKlTpzqX08+8a968ub755hv98ssvkqQtW7ZozZo1at++vSR66S5P9W3dunUKDg5WkyZNnHNuvvlmBQcHX7e9tYoPR/ag48ePKysrS2XLlnUZL1u2rI4cOVJAVRV+xhgNGjRIzZs3V926dSXJ2a/cerlv3z7nHF9fX5UqVSrHnOup37Nnz9bGjRu1YcOGHMvoY/7s3r1bU6ZM0aBBgzRixAitX79e/fr1k91u14MPPkg/8+Hpp5/W6dOnVbNmTXl5eSkrK0vjxo3T/fffL4mfTXd5qm9HjhxRWFhYju2HhYVdt721ikB1FdhsNpfnxpgcY/ifvn376j//+Y/WrFmTY5k7vbye+n3gwAH1799fX3/9tfz8/C45jz7mjcPhUOPGjfXSSy9Jkho2bKjt27drypQpevDBB53z6OeVzZkzR5988olmzZqlOnXqaPPmzRowYIAiIiLUo0cP5zx66R5P9C23+fTWfVzy86AyZcrIy8srR7o/duxYjv9N4C9PPfWUFi5cqBUrVqhChQrO8fDwcEm6bC/Dw8N14cIFnTx58pJzrnUbN27UsWPH1KhRI3l7e8vb21urVq3Sv/71L3l7ezv7QB/zply5cqpdu7bLWK1atbR//35J/Fzmx9ChQ/XMM8+oa9euqlevnhITEzVw4ECNHz9eEr10l6f6Fh4erqNHj+bY/u+//37d9tYqApUH+fr6qlGjRlq2bJnL+LJly3TLLbcUUFWFkzFGffv21fz585WcnKyoqCiX5VFRUQoPD3fp5YULF7Rq1SpnLxs1aiQfHx+XOSkpKdq2bdt10+9WrVpp69at2rx5s/PRuHFjde/eXZs3b1aVKlXoYz40a9Ysx9t3/PLLL6pcubIkfi7zIy0tTcWKuf6J8fLycr5tAr10j6f61rRpU50+fVrr1693zvnhhx90+vTp67a3lhXEnfDXsuy3Tfjggw/Mjh07zIABA0xAQIDZu3dvQZdWqDzxxBMmODjYrFy50qSkpDgfaWlpzjkTJkwwwcHBZv78+Wbr1q3m/vvvz/WlwRUqVDDLly83P/30k7ntttuu+ZdUX8nFr/Izhj7mx/r16423t7cZN26c+fXXX83MmTONv7+/+eSTT5xz6Gfe9OjRw5QvX975tgnz5883ZcqUMcOGDXPOoZe5O3PmjNm0aZPZtGmTkWRee+01s2nTJufb73iqb+3atTP169c369atM+vWrTP16tXjbRMsIFBdBW+//bapXLmy8fX1NTfeeKPzrQDwP5JyfSQlJTnnOBwOM2rUKBMeHm7sdru59dZbzdatW122c+7cOdO3b19TunRpU7x4cXPHHXeY/fv3/8NHU7j8PVDRx/z54osvTN26dY3dbjc1a9Y077//vsty+pk3qamppn///qZSpUrGz8/PVKlSxYwcOdKkp6c759DL3K1YsSLX3489evQwxniub3/88Yfp3r27CQwMNIGBgaZ79+7m5MmT/9BRXntsxhhTMOfGAAAArg3cQwUAAGARgQoAAMAiAhUAAIBFBCoAAACLCFQAAAAWEagAAAAsIlABAABYRKACAACwiEAF4JrUs2dP2Wy2HI/ffvutoEsDcA3yLugCAOBqadeunZKSklzGQkNDC6gaVxkZGfLx8SnoMgB4CGeoAFyz7Ha7wsPDXR5eXl65zt23b586dOigUqVKKSAgQHXq1NHixYudy7dv366EhAQFBQUpMDBQLVq00K5duyRJDodDY8eOVYUKFWS32xUdHa2lS5c61927d69sNps+++wzxcXFyc/PT5988okkKSkpSbVq1ZKfn59q1qypd9555yp2BMDVwhkqAJDUp08fXbhwQatXr1ZAQIB27NihEiVKSJIOHTqkW2+9VXFxcUpOTlZQUJC+++47ZWZmSpLeeOMNTZo0Se+9954aNmyoDz/8UHfeeae2b9+u6tWrO/fx9NNPa9KkSUpKSpLdbtfUqVM1atQovfXWW2rYsKE2bdqkXr16KSAgQD169CiQPgBwU0F/OjMAXA09evQwXl5eJiAgwPm45557Ljm/Xr16ZvTo0bkuGz58uImKijIXLlzIdXlERIQZN26cy9hNN91knnzySWOMMXv27DGSzOTJk13mVKxY0cyaNctl7IUXXjBNmza94vEBKFw4QwXgmtWyZUtNmTLF+TwgIOCSc/v166cnnnhCX3/9tW6//Xbdfffdql+/viRp8+bNatGiRa73PKWmpurw4cNq1qyZy3izZs20ZcsWl7HGjRs7v/7999914MABPfLII+rVq5dzPDMzU8HBwfk7UAAFjkAF4JoVEBCgatWq5Wnuo48+qrZt2+rLL7/U119/rfHjx2vSpEl66qmnVLx48Suub7PZXJ4bY3KMXRzoHA6HJGnq1Klq0qSJy7xL3ecFoPDipnQA+P8qVqyo3r17a/78+Ro8eLCmTp0qSapfv76+/fZbZWRk5FgnKChIERERWrNmjcv42rVrVatWrUvuq2zZsipfvrx2796tatWquTyioqI8e2AArjrOUAGApAEDBig+Pl433HCDTp48qeTkZGcg6tu3r95880117dpVw4cPV3BwsL7//nvFxMSoRo0aGjp0qEaNGqWqVasqOjpaSUlJ2rx5s2bOnHnZfY4ePVr9+vVTUFCQ4uPjlZ6erg0bNujkyZMaNGjQP3HYADyEQAUAkrKystSnTx8dPHhQQUFBateunV5//XVJUkhIiJKTkzV06FDFxsbKy8tL0dHRzvum+vXrp9TUVA0ePFjHjh1T7dq1tXDhQpdX+OXm0Ucflb+/v1555RUNGzZMAQEBqlevngYMGHC1DxeAh9mMMaagiwAAACjKuIcKAADAIgIVAACARQQqAAAAiwhUAAAAFhGoAAAALCJQAQAAWESgAgAAsIhABQAAYBGBCgAAwCICFQAAgEUEKgAAAIsIVAAAABb9P9PEJ8mhkZ4oAAAAAElFTkSuQmCC\n",
      "text/plain": [
       "<Figure size 640x480 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "# EXtracting variable importance\n",
    "\n",
    "from xgboost import plot_importance\n",
    "plot_importance(xg_reg)\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 116,
   "id": "572ef67d",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Index(['ent', 'tyl_ent', 'ecoli'], dtype='object')"
      ]
     },
     "execution_count": 116,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Revisiting what variables were used for input\n",
    "X_train.columns"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 129,
   "id": "a45e13ed",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Enter value for ent: 5\n",
      "Enter value for tyl_ent: 5\n",
      "Enter value for ecoli: 5\n",
      "Predicted value of tet_ent is:  11.159622\n"
     ]
    }
   ],
   "source": [
    "#Writing a code to ask user input, use the developed model to give instant predictions\n",
    "\n",
    "ent = float(input(\"Enter value for ent: \"))\n",
    "tyl_ent = float(input(\"Enter value for tyl_ent: \"))\n",
    "ecoli = float(input(\"Enter value for ecoli: \"))\n",
    "\n",
    "# Create a DataFrame with the user input\n",
    "user_input = pd.DataFrame({\n",
    "    'ent': [ent],\n",
    "    'tyl_ent': [tyl_ent],\n",
    "    'ecoli': [ecoli]\n",
    "})\n",
    "\n",
    "# Make a prediction for the user input\n",
    "prediction = xg_reg.predict(user_input)\n",
    "\n",
    "# Print the predicted value\n",
    "print(\"Predicted value of tet_ent is: \", prediction[0])\n"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3 (ipykernel)",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.9.13"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}
